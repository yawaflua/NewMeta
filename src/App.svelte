<script>
  import { onMount } from 'svelte';

  let copied = false;
  let menuOpen = false;
  let year = new Date().getFullYear();

  const people = [
    {
      number: '01',
      name: 'ДАРКСИР',
      role: 'АРХИТЕКТОР ХАОСА',
      mark: 'Д',
      quote: 'Ломает правила ещё до того, как их успели придумать.',
      tags: ['MINDSET', 'IMPACT', 'AURA'],
      color: '#d9ff43'
    },
    {
      number: '02',
      name: 'ЧЕН',
      role: 'ДВИГАТЕЛЬ МЕТЫ',
      mark: 'Ч',
      quote: 'Превращает любой мув в единственно верное решение.',
      tags: ['TEMPO', 'STYLE', 'VISION'],
      color: '#b69cff'
    }
  ];

  const principles = [
    ['01', 'НИКАКИХ ТИР-ЛИСТОВ', 'Если в тир-листе нет Дарксира и Чена — проблема в тир-листе.'],
    ['02', 'ТОЛЬКО СВЕЖИЕ МУВЫ', 'Повторять за другими поздно. Мету создают, а не догоняют.'],
    ['03', 'РОФЛ — ЭТО СЕРЬЁЗНО', 'Мы смеёмся громко, но выбор делаем безошибочно.']
  ];

  function scrollToId(id) {
    menuOpen = false;
    document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' });
  }

  async function joinMovement() {
    try {
      await navigator.clipboard.writeText('ДАРКСИР + ЧЕН = НОВАЯ МЕТА');
      copied = true;
      setTimeout(() => (copied = false), 2200);
    } catch {
      scrollToId('manifesto');
    }
  }

  onMount(() => {
    const root = document.documentElement;
    const moveGlow = (event) => {
      root.style.setProperty('--mouse-x', `${event.clientX}px`);
      root.style.setProperty('--mouse-y', `${event.clientY}px`);
    };

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) entry.target.classList.add('is-visible');
        });
      },
      { threshold: 0.12 }
    );

    document.querySelectorAll('.reveal').forEach((element) => observer.observe(element));
    window.addEventListener('pointermove', moveGlow, { passive: true });

    return () => {
      observer.disconnect();
      window.removeEventListener('pointermove', moveGlow);
    };
  });
</script>

<svelte:head>
  <title>NewMeta — Дарксир × Чен</title>
</svelte:head>

<div class="site-shell">
  <header class="nav-wrap">
    <a class="logo" href="#top" aria-label="NewMeta, на главную">
      <svg viewBox="0 0 34 34" aria-hidden="true">
        <path d="M3 25V9l14 8L31 9v16" />
        <path d="M3 9l14 16L31 9" />
      </svg>
      <span>NEWMETA</span>
    </a>

    <nav class:open={menuOpen} aria-label="Основная навигация">
      <button onclick={() => scrollToId('duo')}>ДУЭТ</button>
      <button onclick={() => scrollToId('tournament')}>NEWMETA FB</button>
      <button onclick={() => scrollToId('manifesto')}>МАНИФЕСТ</button>
      <button onclick={() => scrollToId('verdict')}>ВЕРДИКТ</button>
    </nav>

    <div class="nav-status"><i></i> META ONLINE</div>
    <button
      class="menu-button"
      class:active={menuOpen}
      aria-label="Открыть меню"
      aria-expanded={menuOpen}
      onclick={() => (menuOpen = !menuOpen)}
    >
      <span></span><span></span>
    </button>
  </header>

  <main>
    <section class="hero" id="top">
      <div class="hero-grid" aria-hidden="true"></div>
      <div class="hero-eyebrow">
        <span>НЕЗАВИСИМОЕ МЕТА-БЮРО</span>
        <span class="hero-code">NM/001—{year}</span>
      </div>

      <div class="hero-title-wrap">
        <p class="kicker">ОФИЦИАЛЬНО ЗАЯВЛЯЕМ:</p>
        <h1>
          <span>ДАРКСИР <em>×</em> ЧЕН</span>
          <span class="outline">НОВАЯ МЕТА</span>
        </h1>
      </div>

      <div class="hero-bottom">
        <p>
          Два имени. Ноль сомнений.<br />
          Все остальные просто патчноут.
        </p>
        <button class="primary-button" onclick={() => scrollToId('duo')}>
          <span>СМОТРЕТЬ ДОКАЗАТЕЛЬСТВА</span>
          <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6" /></svg>
        </button>
        <div class="scroll-note">
          <span>SCROLL TO UPDATE</span>
          <i></i>
        </div>
      </div>
    </section>

    <div class="ticker" aria-label="Главный тезис NewMeta">
      <div class="ticker-track">
        {#each Array(2) as _}
          <div class="ticker-set">
            <span>ДАРКСИР</span><b>✦</b><span>ЧЕН</span><b>✦</b><span>NEWMETA FB</span><b>✦</b><span>40 СМЕРТЕЙ</span><b>✦</b>
          </div>
        {/each}
      </div>
    </div>

    <section class="duo section-pad" id="duo">
      <div class="section-heading reveal">
        <p class="section-index">[ 01 / НОВАЯ СИЛА ]</p>
        <h2>ДВА ЛИЦА<br />ОДНОЙ <span>МЕТЫ</span></h2>
        <p class="heading-copy">По отдельности — феномены. Вместе — обновление, которое невозможно откатить.</p>
      </div>

      <div class="people-grid">
        {#each people as person, index}
          <article class="person-card reveal" style={`--card-accent:${person.color}; --delay:${index * 100}ms`}>
            <div class="card-topline"><span>{person.number}</span><span>NEW META UNIT</span></div>
            <div class="portrait" aria-hidden="true">
              <div class="portrait-grid"></div>
              <div class="portrait-orbit"></div>
              <span>{person.mark}</span>
              <small>{person.name}</small>
            </div>
            <div class="person-info">
              <p>{person.role}</p>
              <h3>{person.name}</h3>
              <blockquote>«{person.quote}»</blockquote>
              <div class="tags">
                {#each person.tags as tag}<span>{tag}</span>{/each}
              </div>
            </div>
          </article>
        {/each}
      </div>

      <div class="equation reveal">
        <div><small>ЮНИТ 01</small><strong>ДАРКСИР</strong></div>
        <span>+</span>
        <div><small>ЮНИТ 02</small><strong>ЧЕН</strong></div>
        <span>=</span>
        <div class="equation-result"><small>РЕЗУЛЬТАТ</small><strong>NEWMETA</strong></div>
      </div>
    </section>

    <section class="tournament section-pad" id="tournament">
      <div class="tournament-noise" aria-hidden="true"></div>
      <div class="tournament-head reveal">
        <p class="section-index">[ 02 / ТУРНИР ПО ФИДУ ]</p>
        <div class="live-chip"><i></i> ПРОТОКОЛ ЗАВЕРШЁН</div>
      </div>

      <div class="tournament-title reveal">
        <p>FEED BATTLE / SEASON 01</p>
        <h2>NEWMETA <span>FB</span></h2>
        <div class="tournament-subtitle">
          <span>ГЛАВНАЯ ДИСЦИПЛИНА</span>
          <strong>ТИНКЕР / МИД / БЕЗ СТРАХА</strong>
        </div>
      </div>

      <div class="record-board reveal">
        <div class="record-player">
          <span class="record-label">РЕКОРДСМЕН ТУРНИРА</span>
          <h3>НИКИТА<br /><span>КАШИН</span></h3>
          <div class="player-meta">
            <div><small>ГЕРОЙ</small><strong>TINKER</strong></div>
            <div><small>ПОЗИЦИЯ</small><strong>MID</strong></div>
            <div><small>СТАТУС</small><strong>NEW META</strong></div>
          </div>
        </div>

        <div class="death-counter">
          <span class="record-label">ЗАФИКСИРОВАНО СМЕРТЕЙ</span>
          <strong>40</strong>
          <div class="death-meter" aria-label="40 из 40 смертей">
            {#each Array(40) as _, death}
              <i class:milestone={(death + 1) % 10 === 0}></i>
            {/each}
          </div>
          <p>СОРОК. НА МИДОВОМ ТИНКЕРЕ.<br />ЭТО УЖЕ НЕ ФИД — ЭТО МЕТОДОЛОГИЯ.</p>
        </div>
      </div>

      <div class="tournament-route reveal">
        <div><small>01</small><span>ВЫБРАТЬ<br />ТИНКЕРА</span></div>
        <b>→</b>
        <div><small>02</small><span>ПОЙТИ<br />НА МИД</span></div>
        <b>→</b>
        <div><small>03</small><span>УМЕРЕТЬ<br />40 РАЗ</span></div>
        <b>→</b>
        <div class="route-win"><small>GG</small><span>СТАТЬ<br />МЕТОЙ</span></div>
      </div>

      <blockquote class="tournament-quote reveal">
        «Каждая смерть приближала нас к пониманию игры.»
        <span>— ДПРМ / АНАЛИТИЧЕСКИЙ ОТДЕЛ NEWMETA FB</span>
      </blockquote>
    </section>

    <section class="manifesto" id="manifesto">
      <div class="manifesto-inner section-pad">
        <div class="manifesto-head reveal">
          <p class="section-index">[ 03 / МАНИФЕСТ ]</p>
          <p>КОДЕКС ТЕХ, КТО УЖЕ<br />ЖИВЁТ В СЛЕДУЮЩЕМ ПАТЧЕ</p>
        </div>

        <div class="principles">
          {#each principles as principle}
            <article class="principle reveal">
              <span>{principle[0]}</span>
              <h3>{principle[1]}</h3>
              <p>{principle[2]}</p>
              <svg viewBox="0 0 32 32" aria-hidden="true"><path d="M7 25L25 7M10 7h15v15" /></svg>
            </article>
          {/each}
        </div>
      </div>
    </section>

    <section class="verdict section-pad" id="verdict">
      <div class="verdict-label reveal">
        <span>ФИНАЛЬНЫЙ ВЕРДИКТ</span>
        <span>100% CONFIDENCE</span>
      </div>
      <div class="verdict-copy reveal">
        <p>МЕТА — ЭТО НЕ ТО,<br />ЧТО ВЫБИРАЮТ.</p>
        <h2>МЕТА — ЭТО<br /><span>КТО.</span></h2>
      </div>

      <div class="answer reveal">
        <p>И МЫ УЖЕ ЗНАЕМ ОТВЕТ.</p>
        <div class="answer-names"><span>ДАРКСИР</span><i>×</i><span>ЧЕН</span></div>
        <button onclick={joinMovement} class:copied>
          <span>{copied ? 'ТЕЗИС СКОПИРОВАН' : 'ПРИСОЕДИНИТЬСЯ К ДВИЖЕНИЮ'}</span>
          <svg viewBox="0 0 24 24" aria-hidden="true">
            {#if copied}<path d="M5 12l4 4L19 6" />{:else}<path d="M5 12h14M13 6l6 6-6 6" />{/if}
          </svg>
        </button>
      </div>
    </section>
  </main>

  <footer>
    <a class="logo footer-logo" href="#top" aria-label="Наверх">
      <svg viewBox="0 0 34 34" aria-hidden="true"><path d="M3 25V9l14 8L31 9v16" /><path d="M3 9l14 16L31 9" /></svg>
      <span>NEWMETA</span>
    </a>
    <p>РОФЛО-ОРГАНИЗАЦИЯ С СЕРЬЁЗНЫМ ВКУСОМ</p>
    <p>© {year} / META NEVER SLEEPS</p>
  </footer>
</div>
