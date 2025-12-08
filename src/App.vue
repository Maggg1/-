<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const navItems = [
  { id: 'hero', label: 'Home' },
  { id: 'features', label: 'Features' },
  { id: 'experience', label: 'Experience' },
  { id: 'insights', label: 'Insights' },
  { id: 'contact', label: 'Contact' }
]

const footerColumns = [
  {
    title: '&#20135;&#21697;&#26381;&#21153;',
    links: [
      '&#32929;&#31080;&#20132;&#26131;',
      '&#26399;&#26435;&#20132;&#26131;',
      'ETF&#25237;&#36164;',
      '&#26234;&#33021;&#25237;&#39038;',
      '&#24066;&#22330;&#30740;&#31350;'
    ]
  },
  {
    title: '&#20851;&#20110;&#25105;&#20204;',
    links: ['&#20844;&#21496;&#31616;&#20171;', '&#26032;&#38395;&#21160;&#24577;', '&#21512;&#20316;&#20249;&#20276;']
  },
  {
    title: '&#23458;&#25143;&#25903;&#25345;',
    links: [
      '&#24110;&#21161;&#20013;&#24515;',
      '&#36134;&#25143;&#24320;&#31435;',
      '&#36153;&#29992;&#26631;&#20934;',
      '&#23433;&#20840;&#20445;&#38556;',
      '&#32852;&#31995;&#25105;&#20204;'
    ]
  },
  {
    title: '&#27861;&#24459;&#26465;&#27454;',
    links: ['&#38544;&#31169;&#25919;&#31574;', '&#26381;&#21153;&#21327;&#35758;', '&#39118;&#38505;&#25259;&#38706;', '&#21512;&#35268;&#22768;&#26126;']
  }
]

const footerContent = {
  companyName: '&#28023;&#29275;&#25968;&#31185;&#25216;&#26415;',
  tagline: 'Manatee Digital Technology',
  description:
    '&#28023;&#29275;&#25968;&#31185;&#33268;&#21147;&#20110;&#20026;&#20840;&#29699;&#25237;&#36164;&#32773;&#25552;&#20379;&#19987;&#19994;&#12289;&#23433;&#20840;&#12289;&#20415;&#25463;&#30340;&#22269;&#38469;&#37329;&#34701;&#24066;&#22330;&#25237;&#36164;&#26381;&#21153;&#65292;&#36816;&#29992;&#21069;&#27839;&#37329;&#34701;&#31185;&#25216;&#36171;&#33021;&#27599;&#19968;&#20301;&#25237;&#36164;&#32773;&#12290;',
  legal: '&#169; 2025 &#28023;&#29275;&#25968;&#31185;&#25216;&#26415;(&#28145;&#22323;)&#26377;&#38480;&#20844;&#21496; &#29256;&#26435;&#25152;&#26377; | &#31908;ICP&#22791;12345678&#21495;-1',
  address: '&#28145;&#22323;&#24066;&#23453;&#23433;&#21306;&#30887;&#22253;&#21019;&#26234;&#22253;B2&#26635;&#20803;&#21280;&#22346;1&#23618;317'
}

const activeSection = ref(navItems[0].id)
const navOpen = ref(false)
let observer

const toggleNav = () => {
  navOpen.value = !navOpen.value
}

const closeNav = () => {
  navOpen.value = false
}

const handleLinkClick = (id) => {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' })
    closeNav()
  }
}

onMounted(() => {
  // IntersectionObserver keeps the navigation highlight in sync with the visible section.
  observer = new IntersectionObserver(
    (entries) => {
      const visibleEntry = entries
        .filter((entry) => entry.isIntersecting)
        .sort((a, b) => b.intersectionRatio - a.intersectionRatio)[0]

      if (visibleEntry?.target?.id) {
        activeSection.value = visibleEntry.target.id
      }
    },
    {
      root: null,
      rootMargin: '-40% 0px -40% 0px',
      threshold: 0.2
    }
  )

  navItems.forEach(({ id }) => {
    const section = document.getElementById(id)
    if (section) {
      observer.observe(section)
    }
  })
})

onBeforeUnmount(() => {
  observer?.disconnect()
})
</script>

<template>
  <div class="page">
    <nav class="site-nav" :class="{ 'site-nav--open': navOpen }">
      <div class="site-nav__brand" @click="handleLinkClick('hero')">ShopFlow</div>
      <button class="site-nav__toggle" type="button" @click="toggleNav" aria-label="Toggle navigation">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <ul class="site-nav__links">
        <li v-for="item in navItems" :key="item.id">
          <button
            type="button"
            :class="{ 'is-active': activeSection === item.id }"
            @click="handleLinkClick(item.id)"
          >
            {{ item.label }}
          </button>
        </li>
      </ul>
    </nav>

    <main>
      <section id="hero" class="section section--hero">
        <div class="hero__glow" aria-hidden="true">
          <svg
            width="646"
            height="800"
            viewBox="0 0 646 800"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <g filter="url(#filter0_f_1_58)">
              <circle cx="62" cy="225" r="384" fill="#0055FF" fill-opacity="0.15" />
            </g>
            <defs>
              <filter
                id="filter0_f_1_58"
                x="-522"
                y="-359"
                width="1168"
                height="1168"
                filterUnits="userSpaceOnUse"
                color-interpolation-filters="sRGB"
              >
                <feFlood flood-opacity="0" result="BackgroundImageFix" />
                <feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape" />
                <feGaussianBlur stdDeviation="100" result="effect1_foregroundBlur_1_58" />
              </filter>
            </defs>
          </svg>
        </div>
        <img class="hero__map" src="/img/%E5%9C%B0%E5%9B%BE.svg" alt="" aria-hidden="true" />
        <div class="section__content">
          <h1>Design once, sell everywhere.</h1>
          <p class="lead">
            ShopFlow delivers a unified commerce experience with interfaces that flex beautifully from phone to desktop.
            Launch compelling campaigns, streamline checkout, and delight every customer touchpoint.
          </p>
          <div class="hero__actions">
            <button class="cta" type="button" @click="handleLinkClick('features')">Explore Features</button>
            <button class="cta cta--ghost" type="button" @click="handleLinkClick('contact')">Talk to us</button>
          </div>
        </div>
        <div class="section__media">
          <div class="hero-device">
            <img src="/img/%E6%89%8B%E6%9C%BA%201.svg" alt="Mobile dashboard preview" />
            <img
              class="hero-device__overlay"
              src="/img/%E5%9B%BE%E5%B1%82%202%201.svg"
              alt="Analytics spotlight"
            />
          </div>
        </div>
      </section>

      <section id="features" class="section section--features">
        <div class="section__heading">
          <h2>Built for teams that move fast</h2>
          <p>Composable modules let you launch merchandising ideas in hours, not weeks.</p>
        </div>
        <div class="feature-grid">
          <article class="feature-card">
            <h3>Adaptive layouts</h3>
            <p>
              Responsive containers snap into gorgeous breakpoints for phones, tablets, laptops, and wide displays without
              extra code.
            </p>
          </article>
          <article class="feature-card">
            <h3>Unified cart</h3>
            <p>
              Maintain a single cart state across devices so customers can start shopping on mobile and finish at their desk.
            </p>
          </article>
          <article class="feature-card">
            <h3>Campaign-ready blocks</h3>
            <p>
              Drag-and-drop hero banners, product sliders, and CTAs built on top of Vue 3 composition patterns.
            </p>
          </article>
        </div>
      </section>

      <section id="experience" class="section section--experience">
        <div class="section__heading">
          <h2>From strategy to checkout</h2>
          <p>Every touchpoint is optimized to convert visitors into lifelong customers.</p>
        </div>
        <ol class="experience-steps">
          <li>
            <span class="step-number">01</span>
            <div>
              <h3>Plan</h3>
              <p>Define customer journeys and assemble reusable sections tailored to their needs.</p>
            </div>
          </li>
          <li>
            <span class="step-number">02</span>
            <div>
              <h3>Create</h3>
              <p>Leverage prebuilt Vue components to ship stunning visuals with minimal engineering effort.</p>
            </div>
          </li>
          <li>
            <span class="step-number">03</span>
            <div>
              <h3>Refine</h3>
              <p>Measure performance with built-in analytics hooks and optimize continuously.</p>
            </div>
          </li>
        </ol>
      </section>

      <section id="insights" class="section section--insights">
        <div class="section__heading">
          <h2>Commerce insights that drive growth</h2>
          <p>Live dashboards surface the metrics that matter so your team can react instantly.</p>
        </div>
        <div class="insights-grid">
          <div class="insight">
            <span class="insight__value">98%</span>
            <p class="insight__label">Checkout completion when using express flows.</p>
          </div>
          <div class="insight">
            <span class="insight__value">2.5x</span>
            <p class="insight__label">Increase in repeat buyers after personalization rollout.</p>
          </div>
          <div class="insight">
            <span class="insight__value">12 hrs</span>
            <p class="insight__label">Average time to launch seasonal storefront refreshes.</p>
          </div>
          <div class="insight">
            <span class="insight__value">40%</span>
            <p class="insight__label">Reduction in support tickets via guided customer journeys.</p>
          </div>
        </div>
      </section>

      <section id="contact" class="section section--contact">
        <div class="section__content">
          <h2>Let’s build your next release</h2>
          <p>
            Share your roadmap and we’ll tailor a responsive commerce experience that captivates customers on every screen.
          </p>
          <form class="contact-form">
            <label>
              <span>Your name</span>
              <input type="text" name="name" placeholder="Alex Doe" autocomplete="name" />
            </label>
            <label>
              <span>Company email</span>
              <input type="email" name="email" placeholder="you@brand.com" autocomplete="email" />
            </label>
            <label class="contact-form__full">
              <span>Project goals</span>
              <textarea name="goals" rows="4" placeholder="Tell us about the experience you want to create."></textarea>
            </label>
            <button class="cta" type="submit">Request a demo</button>
          </form>
        </div>
        <div class="section__media">
          <div class="contact-card">
            <h3>What you get</h3>
            <ul>
              <li>Guided design workshop</li>
              <li>Device-specific experience review</li>
              <li>Performance and accessibility report</li>
            </ul>
          </div>
        </div>
      </section>
    </main>

    <footer class="site-footer">
      <div class="site-footer__inner">
        <div class="footer__brand">
          <div class="footer__logo" aria-hidden="true">
            <span>MT</span>
          </div>
          <div class="footer__brand-text">
            <h3 class="footer__company" v-html="footerContent.companyName"></h3>
            <p class="footer__tagline">{{ footerContent.tagline }}</p>
            <p class="footer__description" v-html="footerContent.description"></p>
          </div>
        </div>

        <div class="footer__columns">
          <div class="footer__column" v-for="column in footerColumns" :key="column.title">
            <h4 v-html="column.title"></h4>
            <ul>
              <li v-for="link in column.links" :key="link">
                <span v-html="link"></span>
              </li>

            </ul>
          </div>
        </div>
      </div>

      <div class="site-footer__bottom">
        <p v-html="footerContent.legal"></p>
        <p v-html="footerContent.address"></p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.page {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background: linear-gradient(180deg, #f0f7ff 0%, #ffffff 100%);
}

.site-nav {
  position: sticky;
  top: 0;
  z-index: 10;
  display: grid;
  grid-template-columns: auto auto;
  align-items: center;
  padding: 0.75rem 1.5rem;
  background-color: rgba(255, 255, 255, 0.92);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid rgba(16, 48, 73, 0.08);
}

.site-nav__brand {
  font-family: var(--heading-font);
  font-size: clamp(1.4rem, 1.2rem + 1vw, 2rem);
  letter-spacing: 0.04em;
  cursor: pointer;
}

.site-nav__toggle {
  justify-self: end;
  width: 2.5rem;
  height: 2.5rem;
  display: inline-flex;
  flex-direction: column;
  justify-content: center;
  gap: 0.35rem;
  background: none;
  border: 1px solid rgba(16, 48, 73, 0.12);
  border-radius: 0.75rem;
  padding: 0.4rem;
}

.site-nav__toggle span {
  height: 2px;
  width: 100%;
  background-color: #103049;
  transition: transform 0.3s ease, opacity 0.3s ease;
}

.site-nav--open .site-nav__toggle span:nth-child(1) {
  transform: translateY(6px) rotate(45deg);
}

.site-nav--open .site-nav__toggle span:nth-child(2) {
  opacity: 0;
}

.site-nav--open .site-nav__toggle span:nth-child(3) {
  transform: translateY(-6px) rotate(-45deg);
}

.site-nav__links {
  grid-column: 1 / -1;
  list-style: none;
  margin: 0;
  padding: 0;
  display: none;
  flex-direction: column;
  gap: 0.25rem;
}

.site-nav--open .site-nav__links {
  display: flex;
}

.site-nav__links button {
  width: 100%;
  padding: 0.65rem 1rem;
  font-size: 0.95rem;
  text-align: left;
  border: none;
  background: none;
  border-radius: 0.75rem;
  cursor: pointer;
  transition: background-color 0.2s ease, color 0.2s ease;
}

.site-nav__links button:hover,
.site-nav__links button.is-active {
  background-color: rgba(58, 207, 213, 0.12);
  color: #0f7b8f;
}

main {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: clamp(3rem, 2.5rem + 2vw, 5rem);
  padding: 0 clamp(1.25rem, 1rem + 3vw, 6rem) 4rem;
}

.section {
  display: grid;
  gap: clamp(1.5rem, 1.2rem + 1vw, 2.5rem);
  align-items: center;
  border-radius: 1.5rem;
  padding: clamp(2rem, 1.8rem + 1vw, 3.5rem);
  background: white;
  box-shadow: 0 24px 60px rgba(15, 48, 73, 0.08);
}

.section--hero {
  padding: 0;
  margin: 0 calc(50% - 50vw);
  border: none;
  border-radius: 0;
  background: linear-gradient(135deg, rgba(15, 123, 143, 0.1), rgba(58, 207, 213, 0.18));
  box-shadow: none;
  grid-template-columns: 1fr;
  position: relative;
  overflow: hidden;
  z-index: 0;
}

.hero__glow {
  position: absolute;
  top: -10rem;
  left: -18rem;
  width: 40rem;
  max-width: 100%;
  pointer-events: none;
  opacity: 0.8;
  z-index: -1;
}

.hero__glow svg {
  width: 100%;
  height: auto;
}

.hero__map {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(1.2);
  width: clamp(400px, 70vw, 900px);
  max-width: none;
  pointer-events: none;
  opacity: 0.4;
  mix-blend-mode: screen;
  z-index: -2;
}

.hero-device {
  position: relative;
  width: clamp(240px, 45vw, 526px);
  aspect-ratio: 526 / 701;
  margin: 0 auto;
}

.hero-device img {
  display: block;
  width: 100%;
  height: auto;
}

.hero-device__overlay {
  position: absolute;
  width: clamp(120px, 25vw, 143px);
  aspect-ratio: 143 / 179;
  right: clamp(-1.5rem, -2vw, -0.5rem);
  top: clamp(10%, 6vw, 18%);
  filter: drop-shadow(0 20px 35px rgba(15, 123, 143, 0.2));
}

.section__content {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  margin-top: 15%;
  margin-left: clamp(2.5rem, 8vw, 6rem);
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.25em;
  font-size: 0.75rem;
  color: #0f7b8f;
}

h1,
h2,
h3 {
  font-family: var(--heading-font);
  color: #103049;
  margin: 0;
}

h1 {
  font-size: clamp(2.4rem, 2rem + 2vw, 3.6rem);
}

.lead {
  font-size: clamp(1rem, 0.95rem + 0.6vw, 1.25rem);
  color: rgba(16, 48, 73, 0.75);
  margin: 0;
}

.hero__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.cta {
  padding: 0.85rem 1.75rem;
  border-radius: 0.9rem;
  border: none;
  font-weight: 600;
  background: linear-gradient(135deg, #0f7b8f, #3acfd5);
  color: white;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.cta:hover {
  transform: translateY(-1px);
  box-shadow: 0 14px 24px rgba(15, 123, 143, 0.25);
}

.cta--ghost {
  background: transparent;
  border: 1px solid rgba(15, 123, 143, 0.35);
  color: #0f7b8f;
}

.section__media {
  display: flex;
  justify-content: center;
}

.device-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(60px, 1fr));
  gap: 1rem;
  width: 100%;
}

.device {
  border-radius: 1.5rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.75), rgba(15, 123, 143, 0.25));
  padding-top: 140%;
  position: relative;
  box-shadow: inset 0 0 0 2px rgba(16, 48, 73, 0.08);
}

.device::after {
  content: '';
  position: absolute;
  inset: 10%;
  border-radius: 1rem;
  background: rgba(16, 48, 73, 0.12);
}

.device--tablet {
  grid-column: span 2;
}

.device--laptop {
  grid-column: span 2;
  padding-top: 80%;
}

.device--desktop {
  grid-column: span 4;
  padding-top: 55%;
}

.section--features .feature-grid {
  display: grid;
  gap: 1.5rem;
}

.feature-card {
  padding: 1.75rem;
  border-radius: 1.25rem;
  border: 1px solid rgba(16, 48, 73, 0.08);
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 18px 40px rgba(15, 48, 73, 0.06);
}

.feature-card p {
  color: rgba(16, 48, 73, 0.7);
  margin: 0.5rem 0 0;
}

.section--experience {
  background: linear-gradient(120deg, rgba(58, 207, 213, 0.16), rgba(237, 250, 252, 0.95));
}

.experience-steps {
  display: grid;
  gap: 1.5rem;
  margin: 0;
  padding: 0;
  list-style: none;
}

.experience-steps li {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 1.25rem;
  align-items: start;
}

.step-number {
  font-family: var(--heading-font);
  font-size: 1.75rem;
  color: rgba(16, 48, 73, 0.4);
}

.experience-steps h3 {
  margin-bottom: 0.25rem;
}

.experience-steps p {
  margin: 0;
  color: rgba(16, 48, 73, 0.7);
}

.section--insights {
  background: linear-gradient(135deg, rgba(15, 48, 73, 0.05), rgba(58, 207, 213, 0.18));
}

.insights-grid {
  display: grid;
  gap: 1.5rem;
}

.insight {
  padding: 1.5rem;
  border-radius: 1.25rem;
  background: rgba(255, 255, 255, 0.92);
  border: 1px solid rgba(16, 48, 73, 0.08);
}

.insight__value {
  font-family: var(--heading-font);
  font-size: clamp(2.2rem, 1.6rem + 2vw, 3.1rem);
  color: #0f7b8f;
}

.insight__label {
  margin: 0.35rem 0 0;
  color: rgba(16, 48, 73, 0.7);
}

.section--contact {
  background: linear-gradient(160deg, rgba(15, 48, 73, 0.08), rgba(58, 207, 213, 0.14));
}

.contact-form {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem 1.25rem;
  margin-top: 1rem;
}

.contact-form label {
  display: grid;
  gap: 0.5rem;
  font-size: 0.9rem;
}

.contact-form input,
.contact-form textarea {
  border-radius: 0.85rem;
  border: 1px solid rgba(15, 48, 73, 0.2);
  padding: 0.75rem 1rem;
  font: inherit;
  background: rgba(255, 255, 255, 0.95);
}

.contact-form__full {
  grid-column: 1 / -1;
}

.contact-form button {
  justify-self: start;
  margin-top: 0.5rem;
}

.contact-card {
  padding: 1.75rem;
  border-radius: 1.25rem;
  background: rgba(255, 255, 255, 0.92);
  border: 1px solid rgba(16, 48, 73, 0.08);
  box-shadow: 0 18px 40px rgba(15, 48, 73, 0.06);
  width: min(320px, 100%);
}

.contact-card ul {
  margin: 0.75rem 0 0;
  padding-left: 1.2rem;
  color: rgba(16, 48, 73, 0.75);
}

.site-footer {
  margin-top: auto;
  background: linear-gradient(180deg, rgba(230, 242, 249, 0.95) 0%, rgba(245, 250, 253, 0.9) 100%);
  border-top: 1px solid rgba(16, 48, 73, 0.08);
  padding: clamp(2.5rem, 2rem + 2vw, 4rem) clamp(1.5rem, 1rem + 3vw, 6rem) clamp(2rem, 1.5rem + 2vw, 3rem);
  color: rgba(16, 48, 73, 0.72);
  font-size: 0.95rem;
}

.site-footer__inner {
  display: grid;
  row-gap: clamp(2.5rem, 2rem + 2vw, 4rem);
  column-gap: clamp(3rem, 2rem + 4vw, 6rem);
  max-width: 1100px;
  margin: 0 auto;
}

.footer__brand {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: minmax(64px, 80px) 1fr;
  align-items: start;
}

.footer__logo {
  width: 72px;
  height: 72px;
  border-radius: 50%;
  background: linear-gradient(135deg, #0f7b8f, #3acfd5);
  display: grid;
  place-items: center;
  color: #ffffff;
  font-family: var(--heading-font);
  font-size: 1.45rem;
  font-weight: 600;
  box-shadow: 0 16px 30px rgba(15, 123, 143, 0.25);
}

.footer__brand-text {
  display: grid;
  gap: 0.4rem;
}

.footer__company {
  margin: 0;
  font-size: clamp(1.4rem, 1.2rem + 0.8vw, 1.75rem);
  color: #103049;
}

.footer__tagline {
  margin: 0;
  font-weight: 600;
  letter-spacing: 0.02em;
  color: rgba(16, 48, 73, 0.65);
}

.footer__description {
  margin: 0;
  line-height: 1.6;
  color: rgba(16, 48, 73, 0.7);
  max-width: 48ch;
}

.footer__columns {
  display: grid;
  gap: 1.25rem;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
}

.footer__column h4 {
  margin: 0 0 0.75rem;
  font-family: var(--heading-font);
  font-size: 1.05rem;
  color: #103049;
}

.footer__column ul {
  margin: 0;
  padding: 0;
  list-style: none;
  display: grid;
  gap: 0.5rem;
  color: rgba(16, 48, 73, 0.7);
}

.footer__column li span {
  display: inline-block;
}

.site-footer__bottom {
  margin: clamp(2rem, 1.5rem + 2vw, 3rem) auto 0;
  max-width: 1100px;
  border-top: 1px solid rgba(16, 48, 73, 0.1);
  padding-top: 1.5rem;
  text-align: center;
  display: grid;
  gap: 0.4rem;
  color: rgba(16, 48, 73, 0.6);
  font-size: 0.85rem;
}

@media (max-width: 640px) {
  .footer__brand {
    grid-template-columns: 1fr;
  }

  .footer__logo {
    justify-self: start;
  }
}

@media (min-width: 900px) {
  .site-footer__inner {
    grid-template-columns: minmax(260px, 320px) 1fr;
    align-items: start;
  }
}

@media (min-width: 720px) {
  .site-nav {
    grid-template-columns: auto 1fr;
    padding: 1rem 4rem;
  }

  .site-nav__toggle {
    display: none;
  }

  .site-nav__links {
    display: flex;
    justify-content: flex-end;
    flex-direction: row;
    gap: 0.5rem;
    grid-column: auto;
  }

  .site-nav__links button {
    width: auto;
    padding: 0.65rem 1.15rem;
    text-align: center;
  }

  .section--hero {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    align-items: stretch;
  }

  .section__media {
    justify-content: flex-end;
  }

  .section--features .feature-grid {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }

  .insights-grid {
    grid-template-columns: repeat(4, minmax(0, 1fr));
  }
}

@media (min-width: 960px) {
  main {
    padding-inline: clamp(4rem, 2rem + 6vw, 8rem);
  }

  .section {
    gap: 2rem 3rem;
  }

  .experience-steps {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }

  .experience-steps li {
    grid-template-columns: auto;
    text-align: center;
  }

  .experience-steps li div {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
  }

  .contact-form {
    grid-template-columns: repeat(2, minmax(240px, 1fr));
  }
}
</style>
