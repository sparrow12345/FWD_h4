<script>
  import { onMount } from 'svelte';
  const MY_EMAIL = 'm.naser@innopolis.university';
  const FIRST_URL = 'https://fwd.innopolis.app/api/hw2';
  const SECOND_URL = 'https://getxkcd.vercel.app/api/comic';

  let xkcd = {
    img: '',
    title: '',
    alt: '',
    uploaddate: '',
  };

  function getHeader() {
    return {
      'Content-Type': 'application/json',
      Accept: 'application/json',
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Headers': '*',
      'Access-Control-Allow-Credentials': 'true',
      GET: 'OPTIONS',
    };
  }

  function getSearchParams(names, values) {
    const urlSearchParam = new URLSearchParams();
    names.forEach((name, i) => {
      urlSearchParam.append(name, values[i]);
    });
    return urlSearchParam;
  }

  async function callAPIWithSearchParamsForId(url) {
    const response = await fetch(url, { headers: getHeader() });
    const data = await response.text();
    return data;
  }

  async function callAPIWithSearchParamsForImage(url) {
    const response = await fetch(url, { mode: 'cors', headers: getHeader() });
    const data = await response.json();
    return data;
  }

  function buildURL(url, params) {
    return url + '?' + params;
  }

  async function fetchXKCD(email) {
    let urlParamString = '';
    if (email !== null) {
      urlParamString = getSearchParams(['email'], [email]).toString();
    }
    const id = await callAPIWithSearchParamsForId(
      buildURL(FIRST_URL, urlParamString)
    );
    const secondUrlParamString = getSearchParams(['num'], [id]).toString();
    const data = await callAPIWithSearchParamsForImage(
      buildURL(SECOND_URL, secondUrlParamString)
    );
    xkcd = {
      img: data.img,
      title: data.title,
      alt: data.alt,
      uploaddate: new Date().toLocaleDateString(),
    };
  }
  onMount(() => {
    fetchXKCD(MY_EMAIL);
  });
</script>

<main>
  <img src={xkcd.img} alt={xkcd.alt} />
  <h1>{xkcd.title}</h1>
  <h2>Upload Date: {xkcd.uploaddate}</h2>
</main>
