
<script setup>
import { computed, onMounted, onUnmounted, ref } from 'vue'

const isTutor = ref(false)

const subjects = [
  'Maths',
  'GCSE English',
  'French',
  '11+',
  'Piano',
  'A-level Chemistry',
  'Spanish',
  'Physics'
]

const activeSubject = ref(0)

const parentForm = ref({
  role: 'parent',
  firstName: '',
  email: '',
  subject: '',
  consent: false
})

const tutorForm = ref({
  fullName: '',
  email: '',
  subjects: '',
  dbs: '',
  consent: false
})

const parentMessage = ref('')
const tutorMessage = ref('')
const mobileMenuOpen = ref(false)

const currentSubject = computed(() => subjects[activeSubject.value])

let subjectTimer

onMounted(() => {
  subjectTimer = window.setInterval(() => {
    activeSubject.value = (activeSubject.value + 1) % subjects.length
  }, 2600)
})

onUnmounted(() => {
  window.clearInterval(subjectTimer)
})

function scrollTo(id) {
  mobileMenuOpen.value = false
  document.getElementById(id)?.scrollIntoView({
    behavior: 'smooth'
  })
}

function submitParent() {
  parentMessage.value =
    'Thanks — your interest is saved in this preview. Connect the form to MailerLite before launch.'
}

function submitTutor() {
  tutorMessage.value =
    'Thanks for your interest in becoming a founding tutor. Connect the form to MailerLite before launch.'
}
</script>

<template>
  <div class="site-shell">

    <!-- HEADER -->
    <header class="topbar">
      <a class="brand" href="#" aria-label="StudyKite home">
        Study<span>Kite</span><i>✳</i>
      </a>

      <button
        class="menu-toggle"
        @click="mobileMenuOpen = !mobileMenuOpen"
        aria-label="Toggle menu"
      >
        ☰
      </button>

      <nav :class="{ open: mobileMenuOpen }">
        <button @click="scrollTo('parents')">Find a tutor</button>
        <button @click="scrollTo('tutors')">Teach with us</button>
        <button @click="scrollTo('safety')">Safety</button>
        <button class="nav-cta" @click="scrollTo('waitlist')">
          Join the waitlist <span>↗</span>
        </button>
      </nav>
    </header>

    <main>

      <!-- HERO -->
      <section class="hero">
        <div
          class="hero-photo"
          role="img"
          aria-label="Student enjoying a focused study session"
        ></div>

        <div class="hero-shade"></div>

        <div class="hero-content">
          <div class="launch-pill">
            <span></span>
            LAUNCHING EARLY 2027 · UK-WIDE
          </div>

          <p class="eyebrow light">A little help. A big leap.</p>

          <h1>
            Leap ahead in
            <span :key="currentSubject" class="changing-word">
              {{ currentSubject }}
            </span><b>.</b>
          </h1>

          <p class="hero-copy">
            Find a tutor who gets you. Learn with confidence,
            one lesson at a time.
          </p>

          <div
            class="audience-switch"
            role="group"
            aria-label="Choose your StudyKite journey"
          >
            <button
              :class="{ selected: !isTutor }"
              @click="isTutor = false"
            >
              I'm looking for a tutor
            </button>

            <button
              :class="{ selected: isTutor }"
              @click="isTutor = true"
            >
              I'm a tutor
            </button>
          </div>

          <form
            v-if="!isTutor"
            class="quick-form"
            @submit.prevent="scrollTo('waitlist')"
          >
            <div class="quick-form-copy">
              <strong>Find your kind of help.</strong>
              <span>Be first to hear when StudyKite opens.</span>
            </div>

            <button type="submit">
              Join the waitlist <span>→</span>
            </button>
          </form>

          <form
            v-else
            class="quick-form tutor-quick"
            @submit.prevent="scrollTo('tutors')"
          >
            <div class="quick-form-copy">
              <strong>What do you teach?</strong>
              <span>Become one of our founding tutors.</span>
            </div>

            <button type="submit">
              Apply as a founding tutor <span>→</span>
            </button>
          </form>

          <p class="hero-note" v-if="!isTutor">
            Under 18? A parent or guardian can join on your behalf.
          </p>

          <p class="hero-note" v-else>
            For tutors aged 18 and over. Checks are part of the process.
          </p>
        </div>

        <div class="hero-sticker">
          GOOD<br>
          THINGS<br>
          GROW<br>
          HERE <span>✳</span>
        </div>
      </section>

      <!-- TRUST STRIP -->
      <section class="trust-strip" id="safety">
        <div class="trust-intro">
          <span class="eyebrow">LEARNING, WITH PEACE OF MIND</span>
          <h2>Every tutor, <em>checked.</em><br>Properly.</h2>
        </div>

        <div class="trust-item">
          <span class="trust-icon">✓</span>
          <strong>Enhanced DBS<br>checked</strong>
        </div>

        <div class="trust-item">
          <span class="trust-icon">⌕</span>
          <strong>ID<br>verified</strong>
        </div>

        <div class="trust-item">
          <span class="trust-icon">♡</span>
          <strong>References<br>checked</strong>
        </div>

        <div class="trust-item">
          <span class="trust-icon">✳</span>
          <strong>Approved by<br>a real person</strong>
        </div>
      </section>

      <!-- WAITLIST -->
      <section class="waitlist-section section-wrap" id="waitlist">
        <div class="section-heading">
          <span class="eyebrow">GET IN EARLY</span>

          <h2>
            Good things come<br>
            to those who <em>learn.</em>
          </h2>

          <p>
            StudyKite opens in early 2027. Tell us who you are
            and we'll save you a place.
          </p>

          <div class="jump-links">
            <button @click="scrollTo('parents')">
              I'm looking for a tutor ↓
            </button>

            <button @click="scrollTo('tutors')">
              I'm a tutor ↓
            </button>
          </div>
        </div>

        <div class="waitlist-card">
          <div class="card-topline">
            <span>✳ YOUR NEXT CHAPTER STARTS HERE</span>
            <span>01 / 02</span>
          </div>

          <h3>Join the waitlist</h3>
          <p class="muted">A head start on finding the right fit.</p>

          <form @submit.prevent="submitParent">
            <label>
              Who's joining?

              <select v-model="parentForm.role">
                <option value="parent">
                  I'm a parent or guardian
                </option>

                <option value="adult">
                  I'm 18 or over and want lessons for myself
                </option>
              </select>
            </label>

            <p class="small-note">
              Under 18? Ask a parent or guardian to join for you.
              They'll add you to their account.
            </p>

            <label>
              First name

              <input
                v-model="parentForm.firstName"
                required
                placeholder="Your first name"
              >
            </label>

            <label>
              Email address

              <input
                v-model="parentForm.email"
                type="email"
                required
                placeholder="you@example.com"
              >
            </label>

            <label>
              What subject do you need?
              <span class="optional">(optional)</span>

              <input
                v-model="parentForm.subject"
                placeholder="e.g. GCSE Maths"
              >
            </label>

            <label class="consent">
              <input
                v-model="parentForm.consent"
                type="checkbox"
                required
              >

              <span>
                I confirm I'm 18 or over, and I'm happy to get
                emails about StudyKite's launch.
              </span>
            </label>

            <button class="button-primary" type="submit">
              Save my place <span>→</span>
            </button>

            <p v-if="parentMessage" class="form-message">
              {{ parentMessage }}
            </p>

            <p class="fine-print">
              Free to join. Unsubscribe any time.
              <a href="mailto:hello@tutaroo.co.uk?subject=Privacy%20enquiry">
                Privacy questions
              </a>
            </p>
          </form>
        </div>
      </section>

      <!-- SUBJECT TICKER -->
      <section class="subjects-band">
        <div class="ticker-label">
          ONE PLACE FOR<br>
          EVERY KIND OF<br>
          BRIGHT IDEA <span>✳</span>
        </div>

        <div class="ticker-window">
          <div class="ticker-track">
            <span
              v-for="n in 2"
              :key="n"
              class="ticker-set"
            >
              <b
                v-for="subject in [
                  'Maths',
                  'English',
                  'Science',
                  '11+',
                  'GCSE',
                  'A-level',
                  'Languages',
                  'Music',
                  'Adult learners'
                ]"
                :key="n + subject"
              >
                {{ subject }} <i>✳</i>
              </b>
            </span>
          </div>
        </div>
      </section>

      <!-- PARENTS -->
      <section class="split-section section-wrap" id="parents">
        <div class="split-copy">
          <span class="eyebrow">FOR PARENTS AND LEARNERS</span>

          <h2>
            Find a tutor<br>
            you can <em>trust.</em>
          </h2>

          <p class="lead">
            The right tutor can change how learning feels.
            Find someone who makes things click.
          </p>

          <ul class="tick-list">
            <li>
              Every tutor DBS and ID checked, and approved by a person
            </li>

            <li>
              Every subject, from 11+ and GCSE to A-level,
              languages and music
            </li>

            <li>
              Safe online lessons that parents can join at any time
            </li>

            <li>
              Waitlist families hear first when we open
            </li>
          </ul>

          <button
            class="button-primary"
            @click="scrollTo('waitlist')"
          >
            Find your tutor <span>→</span>
          </button>
        </div>

        <div class="photo-card parent-photo">
          <div class="photo-caption">
            <span>THE RIGHT SUPPORT</span>
            <strong>Small steps.<br>Big confidence.</strong>
          </div>
        </div>
      </section>

      <!-- HOW IT WORKS -->
      <section class="how-section">
        <div class="section-wrap">
          <div class="center-heading">
            <span class="eyebrow">SIMPLE AS 1, 2, 3</span>

            <h2>
              A better way<br>
              to <em>learn together.</em>
            </h2>
          </div>

          <div class="steps-grid">
            <article class="step-card">
              <span class="step-number">01</span>
              <div class="step-icon">⌕</div>
              <h3>Search and message.</h3>
              <p>
                Compare checked tutors and ask them anything
                before you decide.
              </p>
            </article>

            <article class="step-card">
              <span class="step-number">02</span>
              <div class="step-icon">♡</div>
              <h3>Book and pay securely.</h3>
              <p>
                Arrange lessons and pay through StudyKite,
                not cash in hand.
              </p>
            </article>

            <article class="step-card">
              <span class="step-number">03</span>
              <div class="step-icon">✳</div>
              <h3>Learn with confidence.</h3>
              <p>
                Enjoy safe online lessons, with parents
                able to drop in any time.
              </p>
            </article>
          </div>
        </div>
      </section>

      <!-- TUTORS -->
      <section class="split-section tutor-section section-wrap" id="tutors">
        <div class="photo-card tutor-photo">
          <div class="photo-caption">
            <span>FOR GREAT TEACHERS</span>
            <strong>Do what you do<br>best. We'll help.</strong>
          </div>
        </div>

        <div class="split-copy">
          <span class="eyebrow">FOR TUTORS</span>

          <h2>
            Become a<br>
            founding <em>tutor.</em>
          </h2>

          <p class="lead">
            Spend less time chasing work and more time doing
            what you love: helping people learn.
          </p>

          <ul class="tick-list">
            <li>
              Get booked, not buried: a profile that does the selling for you
            </li>

            <li>
              Clear, reliable payments with no chasing invoices
            </li>

            <li>
              Keep more of what you earn
              <span class="optional">(fees to be confirmed)</span>
            </li>

            <li>
              Get in early and help shape StudyKite
            </li>
          </ul>

          <button
            class="button-primary"
            @click="scrollTo('tutor-form')"
          >
            Apply to teach <span>→</span>
          </button>
        </div>
      </section>

      <!-- TUTOR APPLICATION -->
      <section class="tutor-form-section" id="tutor-form">
        <div class="section-wrap tutor-form-layout">
          <div>
            <span class="eyebrow">YOUR EXPERIENCE MATTERS</span>

            <h2>
              Let's make<br>
              learning <em>better.</em>
            </h2>

            <p class="lead">
              We're looking for brilliant tutors to join us
              at the beginning.
            </p>
          </div>

          <div class="waitlist-card tutor-card">
            <div class="card-topline">
              <span>✳ FOUNDING TUTOR INTEREST</span>
              <span>02 / 02</span>
            </div>

            <h3>Apply for early access</h3>

            <form @submit.prevent="submitTutor">
              <label>
                Full name

                <input
                  v-model="tutorForm.fullName"
                  required
                  placeholder="Your full name"
                >
              </label>

              <label>
                Email address

                <input
                  v-model="tutorForm.email"
                  type="email"
                  required
                  placeholder="you@example.com"
                >
              </label>

              <label>
                Subjects and levels you teach

                <input
                  v-model="tutorForm.subjects"
                  required
                  placeholder="e.g. A-level Chemistry, GCSE Biology"
                >
              </label>

              <label>
                Do you have an Enhanced DBS check?

                <select v-model="tutorForm.dbs" required>
                  <option disabled value="">
                    Choose an option
                  </option>

                  <option>Yes, on the Update Service</option>
                  <option>Yes, not on the Update Service</option>
                  <option>Not yet</option>
                </select>
              </label>

              <label class="consent">
                <input
                  v-model="tutorForm.consent"
                  type="checkbox"
                  required
                >

                <span>
                  I'm 18 or over, and I'm happy to get emails
                  about joining StudyKite.
                </span>
              </label>

              <button class="button-primary" type="submit">
                Apply to be a founding tutor <span>→</span>
              </button>

              <p v-if="tutorMessage" class="form-message">
                {{ tutorMessage }}
              </p>

              <p class="fine-print">
                No commitment yet. We'll send next steps before launch.
              </p>
            </form>
          </div>
        </div>
      </section>

      <!-- FAQ -->
      <section class="faq-section section-wrap">
        <div>
          <span class="eyebrow">GOOD QUESTIONS</span>

          <h2>
            Curious?<br>
            <em>Good.</em>
          </h2>
        </div>

        <div class="faq-list">
          <details open>
            <summary>When does StudyKite launch?</summary>
            <p>
              We're aiming to launch in early 2027 across the UK.
              Join the waitlist to hear updates first.
            </p>
          </details>

          <details>
            <summary>How are tutors checked?</summary>
            <p>
              Our planned checks include Enhanced DBS, identity
              and references, with every tutor reviewed by a real
              person before going live.
            </p>
          </details>

          <details>
            <summary>Can under-18s join the waitlist?</summary>
            <p>
              For safety, a parent or guardian aged 18 or over
              should join on their behalf and add them to their account.
            </p>
          </details>

          <details>
            <summary>Which subjects will be available?</summary>
            <p>
              We're planning support across Maths, English,
              Science, 11+, GCSE, A-level, languages, music and more.
            </p>
          </details>
        </div>
      </section>

      <!-- ORANGE BANNER -->
      <section class="orange-banner">
        <span>✳</span>
        <p>FROM STUCK<br>TO <em>SORTED.</em></p>
        <span>✳</span>
      </section>

    </main>

    <!-- FOOTER -->
    <footer class="footer">
      <a class="brand footer-brand" href="#">
        Study<span>Kite</span><i>✳</i>
      </a>

      <p>Helping everyone take their next leap.</p>

      <div>
        <button @click="scrollTo('parents')">Find a tutor</button>
        <button @click="scrollTo('tutors')">Teach with us</button>
        <button @click="scrollTo('safety')">Safety</button>
        <a href="mailto:hello@tutaroo.co.uk">Contact</a>
      </div>

      <small>
        © 2026 StudyKite. All rights reserved.
      </small>
    </footer>

  </div>
</template>
