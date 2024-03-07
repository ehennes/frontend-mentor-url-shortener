<script setup>
import { ref } from 'vue';
import ButtonMain from './ButtonMain.vue';

const userProvidedLink = ref('');

const urlList = ref([]);

const isValid = ref(false);

const url = 'https://api.tinyurl.com/create';
async function getShortURL(url = '', data = {}) {
    const response = await fetch(url, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        referrerPolicy: 'no-referrer',
        body: JSON.stringify(data)
    });
    return response.json();
}

// handle form submission 
const handleSubmit = (e) => {
    e.preventDefault();

    // check if user input is empty or an invalid url
    checkValidation();

    if (isValid.value) {
        document.querySelector('input:required').style.border = 'none';
        document.querySelector('.error-msg').style.display = 'none';

        // run function to hit tiny url endpoint and return a shortened url 
        getShortURL(`${url}?api_token=${import.meta.env.VITE_TINYURL_API_KEY}`, { url: userProvidedLink.value })
            .then((data) => {
                urlList.value.unshift([userProvidedLink.value, data.data.tiny_url]);

                // save userProvidedLink and shortened url to localStorage
                saveUrlsToStorage(urlList.value);
            })
            .catch((error) => {
                console.log('Error: ', error);
            });

            // remove any button styling when new list item is added 
            const resultButtons = document.querySelectorAll('.result button');

            resultButtons.forEach((button) => {
                button.classList.remove('copied-text-button');
                button.textContent = "Copy";
            });
    } else {
        document.querySelector('input:required').style.border = '2px solid var(--red)';
        document.querySelector('.error-msg').style.display = 'block';
    }
}

const saveUrlsToStorage = (list) => {
    list.forEach((item, index) => {
        if (list.length) {
            localStorage.setItem(`list-${index}`, JSON.stringify(item));
        }
    });
}

const retrieveUrlsFromStorage = () => { 
    for (let i = 0; i < localStorage.length; i++) {
        urlList.value.unshift(JSON.parse(localStorage.getItem(localStorage.key(i))));
    };
}

const checkValidation = () => {
    const urlPattern = /^(https?|ftp):\/\/(([a-z\d]([a-z\d-]*[a-z\d])?\.)+[a-z]{2,}|localhost)(\/[-a-z\d%_.~+]*)*(\?[;&a-z\d%_.~+=-]*)?(#[-a-z\d_]*)?$/i;
    
    if (userProvidedLink.value.length && urlPattern.test(userProvidedLink.value)) {
        isValid.value = true;
    } else {
        isValid.value = false;
    }
}

const copyText = async (text, e) => {
    const resultButtons = document.querySelectorAll('.result button');

    resultButtons.forEach((button) => {
        button.classList.remove('copied-text-button');
        button.textContent = "Copy";
    });

    try {
        await navigator.clipboard.writeText(text);
        e.target.textContent = "Copied!";
        e.target.classList.add('copied-text-button');
    } catch (err) {
        console.error('Failed to copy: ', err);
    }
}

retrieveUrlsFromStorage();

</script>

<template>
    <div class="form-container">
        <form id="link-form" method="post">
            <input name="full-url" v-model="userProvidedLink" type="url" placeholder="Shorten a link here..." required />
            <label class="error-msg">Please add a valid link</label>
            <input type="submit" value="Shorten it!" @click="handleSubmit" />
        </form>
    </div>
    <div v-if="urlList.length" class="results-container"> 
        <div v-for="list in urlList" :key="list.index" class="result">
            <p class="full-url">{{ list[0] }}</p>
            <p class="short-url">{{ list[1] }}</p>
            <ButtonMain class="results-button" @click="(e) => copyText(list[1], e)" :btnAlt=true>
                Copy
            </ButtonMain>
        </div>
    </div>
</template>

<style scoped lang="scss">
    .form-container {
        background-color: var(--violet);
        background-image: url('./../../images/bg-shorten-desktop.svg');
        background-repeat: no-repeat;
        background-size: cover;
        border-radius: 5px;
        position: relative;

        &:before {
            background: #fff;
            content: '';
            height: inherit;
            inset: 0;
            left: 50%;
            position: absolute;
            transform: translate3d(-50%, 0, 0);
            width: 100vw;
            height: 50%;
            z-index: -1;
        }

        form {
            display: flex;
            gap: 25px;
            justify-content: center;
            padding: 50px;
            position: relative;

            input {
                border: none;
                border-radius: 5px;
                font-family: 'Poppins', sans-serif;
                padding: 10px 20px;

                &[type="url"] {
                    flex-basis: 90%;
                    font-size: 18px;
                }

                &[type="submit"] {
                    background: var(--cyan);
                    color: #fff;
                    cursor: pointer;
                    flex-basis: 10%;
                    font-size: 16px;
                    font-weight: 700;
                    transition: all ease 0.3s;

                    &:hover {
                        background: var(--cyan-hover);
                    }
                }
            }

            .error-msg {
                bottom: 0;
                color: var(--red);
                display: none;
                font-size: 16px;
                font-style: italic;
                left: 50px;
                position: absolute;
                transform: translate3d(0, -50%, 0);
            }
        }   
    }

    .result {
        align-items: center;
        background: #fff;
        border-radius: 5px;
        display: flex;
        gap: 20px;
        justify-content: space-between;
        margin-top: 20px;
        padding: 20px 25px;

        p {
            font-weight: 500;
            margin: 0;
        }
        .full-url {
            color: var(--dark-violet);
            flex-basis: 80%;
        }

        .short-url {
            color: var(--cyan);
        }

        button {
            transition: background-color ease 0.3s;

            &.copied-text-button {
                background-color: var(--dark-violet);
            }
        }
    }

    // media queries 
    // 800px and below 
    @media only screen and (max-width: 800px) {
        .form-container {
            form {
                flex-direction: column;
                padding: 25px;

                .error-msg {
                    left: 0;
                    position: relative;
                    text-align: center;
                    transform: translate3d(0, 0, 0);
                }
            }
        }

        .result {
            align-items: start;
            flex-direction: column;

            p {
                word-wrap: anywhere;
            }
        }
    }
</style>