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
  <script lang="ts">
    import { onMount } from "svelte";
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
  
  <div id="app">
    <header>
      <h1>Majed Naser Personal Website</h1>
      <nav>
        <ul>
          <li><a href="#about-me">About Me</a></li>
          <li><a href="#skills">Skills</a></li>
          <li><a href="#projects">Projects</a></li>
          <li><a href="#experience">Experience</a></li>
          <li><a href="#education">Education</a></li>
          <li><a href="#contact">Contact</a></li>
          <li><a href="#XKCD_Image">XKCD</a></li>
        </ul>
      </nav>
    </header>
    <main>
      <section id="about-me">
        <h2>About Me</h2>
        <p>Data Scientist, Software Developer, 
          with a growing thirst for knowledge, and a never-ending passion for IT.</p>
      </section>
      <section id="skills">
        <h2>Skills</h2>
        <ul>
          <li>Languages: C/C++, C#, Java, Python, JavaScript, bash, Solidity</li>
          <li>Frameworks/Libraries: React JS, Pandas, NumPy, Matplotlib, Sci-Kit learn</li>
          <li>Tools: Version Control (Git), VS Code, Jupyter Notebook</li>
          <li>Spoken languages: Arabic - Native, English – Fluent, French – Intermediate, Russian – Beginner</li>
        </ul>
      </section>
      <section id="projects">
        <h2>Projects</h2>
        <ul>
          <li>
            <h3>Movie Website Interface                                                 /Jul, 2022/</h3>
            <p>
              The main goal of this project was to showcase what I learned about React JS in the first few weeks. This project
              features a movie website interface that I have built from scratch.
            </p>
          </li>
          <li>
            <h3>Recommendation System - Recommending best games from user history       /Apr, 2022/</h3>
            <p>The main goal of this project was to build a recommendation system that builds personalized game
              recommendations for a closed set of users (in this task, we assume that the user database will not receive new
              elements later on). The model built uses Singular Value Decomposition (SVD) to achieve the task at hand.
            </p>
            <p>This project was a test task for my internship in Data Science (added in the next section).</p>
          </li>
        </ul>
      </section>
      <section id="experience">
        <h2>Experience</h2>
        <ul>
          <li>
            <h3>Game Developer | Internship      June 2021 – July 2021</h3>
            <p>
              Worked under the umbrella topic “Fun with Formal Methods”, the goal of which was to find more fun ways to teach
              basic mathematical concepts needed for IT Specialists.</p>
            <p>Implemented a small-size entertaining finite-position game borrowed from Math contests to engage people with
              the background part of game theory, Finite Positional Analysis in particular.</p>
          </li>
          <li>
            <h3>Data Scientist | Internship      June 2022 – July 2022</h3>
            <p>The goal of this internship was to build a model that predicts a student’s success or failure in a particular college
              course, taking into account the student’s grade history and the course characteristics and prerequisites.
            </p>
            <p>My role was in Data Extraction and Preprocessing. I used BeautifulSoup library to scrape the data we need from
              our university’s EduWiki website. After that, I processed the data so that it could be used to build the ML model.</p>
          </li>
        </ul>
      </section>
      <section id="education">
        <h2>Education</h2>
        <ul>
          <li>
            <h3>Bachelor's Degree - Innopolis University</h3>
            <p>Earned a Bachelor's degree from Innopolis University with 4.2 GPA</p>
          </li>
          <li>
            Main coursework: Data Structures and Algorithms, Introduction to AI, Software Systems Analysis and Design,
          Computer Architecture, Operating Systems, Linear Algebra, Mathematical Analysis, Probabilities & Statistics.
          </li>
        </ul>
      </section>
      <section id="contact">
        <h2>Contact</h2>
        <ul>
          <li>
            <img src="icons/github.png" width="15" height="18" style="vertical-align:bottom">
            <a id="gh-link" href="https://github.com/sparrow12345">
              GitHub
            </a>
          </li>
          <li>
            <img src="icons/telegram.png" width="15" height="18" style="vertical-align:bottom">
            <a id="tg-link" href="https://t.me/Isildur_son_of_Elendil">
              Telegram
            </a>
          </li>
          <li>
            <img src="icons/google.png" width="15" height="18" style="vertical-align:bottom">
            <a id="email" href="mailto:majdnaser2013@gmail.com">
              Email
            </a>
          </li>
        </ul>
      </section>
    </main>
    <footer>
      <p>Copyright &copy; 2023 by Software Developer</p>
    </footer>
  </div>
</main>
