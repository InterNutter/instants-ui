<template>
  <!-- Please comment like an obsessive-compulsive writing for a scared idiot who's forgotten what all this is for. Kthxbai -->
  <v-app>
    <v-app-bar app>
      <v-app-bar-nav-icon @click="hamburger"></v-app-bar-nav-icon>
      <v-toolbar-title>Mobile Instants</v-toolbar-title>
      <!-- Options for Drawer: Nav by Calendar. Nav by Story Number. Nav by tag. FAQ. [Sign in. Sign up] -->
      <!-- Perma-visible are: First, Prev, Next, Last -->
    </v-app-bar>

    <v-navigation-drawer app temporary bottom
                         v-model="drawer"
    >

      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">
            Mobile Instants
          </v-list-item-title>
          <v-list-item-subtitle>
            Free stories for you, every day of the year.
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list
          dense
          nav
      >
        <v-list-item
            v-for="item in getItems"
            :key="item.title"
            link
            @click.stop="perform(item.action)"
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <v-container fluid>
        <!-- Settings nonsense: create account, login, aesthetics, faves, donations todo LATER -->
        <div v-if='mode==="donate"'>
          <h4 class="text-h4">Support the App, the Author, and the Team</h4>
          <p>Even though this app is free and you can access any of my stories at any time, I am still a mortal being who needs frivolous things like... food.</p>
          <p>As such, and without any obligation on your part, if you would like to support the author and the app team in having nice things, please consider donating.</p>
          <v-row>
            <v-col :md="6" :sm="12" class="d-flex flex-column">
              <v-card class="flex d-flex flex-column">
                <v-card-title>Ko-fi</v-card-title>
                <v-card-subtitle>
                  One-time donation, minimum $3
                </v-card-subtitle>
                <v-card-text>
                  Ko-fi is a less evil, more cuddly donations platform that allows all users to use any name they like, without being linked to the name on your credit card. It allows for single, non-recurring donations.
                </v-card-text>
                <v-card-actions>
                  <v-btn class="primary" @click.stop="gotoURL('https://ko-fi.com/cmweller')">
                    <v-icon left>mdi-cup</v-icon> Donate
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-col>
            <v-col :md="6" :sm="12" class="d-flex flex-column">
              <v-card class="flex d-flex flex-column">
                <v-card-title>Patreon</v-card-title>
                <v-card-subtitle>
                  Regular monthly donation, minimum $1
                </v-card-subtitle>
                <v-card-text>
                  Patreon is the defacto donation platform for creative peoples world-wide. Depending on how much you are willing to donate per month, you have access to all kinds of exclusive donor-only perks, and previews of some of my more exciting content before the rest of the universe.
                </v-card-text>
                <v-card-actions>
                  <v-btn class="primary" @click.stop="gotoURL('https://www.patreon.com/cmweller')">
                    <v-icon left>mdi-patreon</v-icon> Donate
                  </v-btn>
                </v-card-actions>

              </v-card>
            </v-col>
          </v-row>
        </div>
        <div v-else-if="mode==='faq'">
          <!-- I have been adding these as they occurred to me. Reorder so they make sense? -->
          <h2>Most of your questions... answered.</h2>
          <p><b>What is this, anyway?</b><br />
            This is an all-access application for you to be able to read <i>any</i> of the literal thousands of flash fictions as written by one author throughout the years.<br />
            It's also a massive database of literally thousands of flash fictions as written by one author over the years.
          </p>
          <p><b>Just one author wrote all of these?</b><br />
            Yes. Starting sometime in January 2013, the author C. M. Weller challenged hir readers to stump them whilst also prompting a flash fiction. No holds were expected to be barred, but time has discovered some limits.<br />
            Since then, there has been a fresh story written every day except Christmas, which is their day off.
          </p>
          <p><b>Hold up, was that a <i>neopronoun</i>?</b><br />
            Please don't say that with a sneer. Yes, C. M. Weller uses a neopronoun. They prefer ze/hir from the even dozen currently accepted neopronouns available. Mostly because this is the one ze can conjugate without excess thought.<br />
            It began as a social experiment, to see how far hir writing could get on its own merit without gender entering the mix. It took some time, but C. M. has come to the realisation that being agender is kind'a cool, actually.
          </p>
          <p><b>How could gender enter into things? Anyone can write books now.</b><br />
            That's a nice assumption you've got there.<br />
            Here's an experiment that may blow your mind:</p>
            <ol>
              <li>Go to your nearest bookstore</li>
              <li>Head into the fiction section</li>
              <li>Do a quick census of authors by genre, noting the definitively male names, the definitively female names, and the ones where you can't immediately tell</li>
              <li>Eliminate any works in an established franchise owned by a corporation</li>
              <li>The science fiction genre will have predominately male names</li>
              <li>The romance genre will have predominately female names</li>
              <li>The drama genre may well be evenly mixed</li>
            </ol><br />
          <p>
            So yes, there is a bias in fiction. Specifically in which genre "belongs" to which gender.
          </p>
          <p><b>Agender? Neopronouns? What <i>is</i> this?</b><br />
            Hello. This is the twenty-first century. Change is the nature of time.<br />
            Now that the gays can get married in a few places, there's people who'd like to be fully themselves. This includes a spectrum of genders and sexualities between consenting adults.<br />
            To paraphrase the original text of <i>Peter Pan</i> about the fairies... "Some are boys, some are girls, and some are little sillies who don't know what they are."<br />
            C. M is fully at home with being a silly of any dimensions, by the way.<br />
            To explain hirself and hirself only, ze may be comfortable with the gender ze presented at birth, but neither of the traditional binary options thrill me to extremes. Not gender euphoria, nor gender dysphoria, but rather... gender meh.<br />
            Ze feels "meh" about hir own gender. It's a thing. It may only be <i>hir</i> thing, but it is a thing.
          </p>
          <p><b>Okay, so what's up with the calendar?</b><br />
            We need to explain a few things.<br />
            As mentioned above, this started sometime towards the beginning of 2013 with no bold visions of the future. C. M. thought they'd do this for the doddle and it would fizzle out in a few months either from boredom or disinterest.<br />
            Oh boy howdy was ze wrong about that.<br />
            Six years after that, ze had the bright idea to have an app that would allow readers to see any of hir stories anywhere.<br />
            <i>And then the plague happened...</i><br />
            So hir brain imploded and combined with procrastination, ze missed out on the time to use an easier programming language, and now ze relies on hir Best Beloved to help hir with the tricky bits of this thing.<br />
            C. M. has made problems for hirself without intent. So because ze didn't start on January First, 2013, and because of taking a day off every Christmas, the day of the story is not the actual day of publication.<br />
            We're trying to make things as easy to use as possible, but there's always the chance for technical issues.
          </p>
          <p><b>Who is 'we'?</b><br />
            Currently [2021], there are two people running this app.<br />
            C. M. Weller, the literary brains behind the curtain. <br />
            And their Best Beloved, norganna, late of <i>Auctioneer</i> fame. They're the code genius doing most of the heavy lifting.<br />
            There may or may not be more as time passes. The budget is always the problem with something like this.
          </p>
          <p><b>Speaking of budget... how do you expect to make money from this?</b><br />
            Short answer: we don't.<br />
            C. M. has posted these stories for free for <i>years</i>. It would be unfair to demand money at this stage in the game.<br />
            Therefore, giving them money for this app, even in ads, would be a scummy move.<br />
            Donations and funding should be both voluntary and with full options. If you <i>want</i> to give us money, that should be your choice.<br />
            C. M. has grown to abhor advertising in free apps, so that's a factor too.
          </p>
          <p><b>If it's free, why is there an account I could have?</b><br />
            That's there so you can customise your reading experience.<br />
            We aim to have full availability of readability options, including colours of text and background so you don't burn your eyes out reading black text on a white background.<br />
            In the fullness of time, we shall have font choices, font size options, and maybe even a robot to read to you. Some goals will be easier to reach than others. Bear with us.<br />
            There will also be an option to collect your favourites.<br />
            We want as many people as possible reading these things, so accessibility is a priority. But since there's only two of us, it might take a bit of a while.
          </p>
          <p><b>Are there donation rewards?</b><br />
            In brief: sort of.<br />
            The donations page is more or less a link to two fundraisers I already have going: Ko-fi and Patreon.<br />
            Donors on Ko-fi will have a variant of their name or internet handle used as a character in a fresh Instant, as well as thanks for their kind donation as a postscript.<br />
            Sponsors on Patreon will gain access to Patreon content according to their tier.<br />
            For those worried about the "variant" part - C. M. Weller will take a part of or a variation of the name given in Ko-fi to use as a character in an Instant. There is no guarantee that that variant name will not turn up as a villain in fiction.<br />
            Rest assured, all the same, that you are a hero to us.
          </p>
          <p><b>I didn't like a story!</b><br />
            Well, they can't all be winners.<br />
            Some of them were written before C. M. learned about certain things. Some are indeed products of their time. Some are... very angry indeed about certain things. Some are truly gross. Some will confront you with new concepts. That's okay.<br />
            What's not okay is getting violent at a person because a work of fiction upset your world view.<br />
            Also, it's nice to remember that works of fiction do not necessarily reflect <i>all</i> the views of the author. Some stories encompass unpleasant material, and you are never obligated to read anything here.<br />
            There's literally thousands of stories here. There's bound to be something you like. And if not, there's no guilt at all in uninstalling the app.
          </p>
          <p><b>I don't like you!</b><br />
            Bit of a shame. We can't all get along, and that's okay.<br />
            You have your reasons for your anger, and the stories here are the most likely contributing factor. Yes, C. M. has made mistakes. Yes, C. M. tries to learn from them.<br />
            Just remember that people on the internet are as real as you are and have the same rights to live, laugh, and love as you do.<br />
            You have the right to disagree with C. M.'s stories, hir identity, and hir lifestyle as you imagine it. What you do not have is the right to end that life. That's murder, dear reader, and illegal everywhere.<br />
            Nevertheless, C. M. shall continue to exist regardless of your opinion on the matter.
          </p>
          <p><b>I loved this so much I made/want to make a derivative work! Is that okay?</b><br />
            Derivative works - better known as fanart, fanfictions, or fanvideos - are the seeds of anything creative. Just as C. M. started with fanfiction, ze sees nothing wrong with derivative works.<br />
            <i>However...</i><br />
            There's legal difficulty with showing an author something that <i>builds</i> on an extant work. Anything you say to or show an author can be taken in and used in a later work. This is trouble when money comes into the picture<br />
            Lawsuits have been made of less. You can make what you want, but please don't send C. M. anything that could build on their universes unless it is an actual prompt for an Instant.<br />
            Also, please don't send hir anything you wouldn't be comfortable showing your maiden aunt. Just as a general rule.
          </p>
          <p><b>Where <i>do</i> I send prompts?</b><br />
            Glad you asked!<br />
            C. M. Weller runs a <a href="https://www.internutter.org/bb/category/6/prompts">small forum</a> where readers can send in story ideas. Just keep in mind that the shorter the idea, the better the story.<br />
            There will be no instant stories resulting from any prompt starting with "can you write a book--". The point of the <i>daily</i> flash fictions is a <i>brief</i> writing exercise that shouldn't take more than a few hours.<br />
            It takes C. M. Weller <i>ten months</i> to write a novel.
          </p>
          <p><b>I could write better stuff than any of this!</b><br />
            Please do. C. M. welcomes the competition.<br />
            You can even use any of the past prompts to do that.<br />
            There's sites like Peakd that will allow you to see how well those stories do from day to day. It takes time, patience, and daily content to get a regular following, and a lot of effort to make an app like this.<br />
            That said, writing a daily flash fiction has helped C. M. overcome the spectre of Writer's Block. Until the 2020 mental meltdown, there were never any gaps in their creative output. Even <i>then</i>, C. M. still maintained the daily flash fictions.
          </p>
          <p><b>What does the "C. M." stand for?</b><br />
            C. M. Weller prefers that no assumptions about the quality of hir writing be made as a result of any gender prejudice.<br />
            There's very few names that don't have gender assumptions packaged with them, so ze uses hir initials.<br />
            Therefore, the answer to that question is completely moot.
          </p>
          <p><b>Where can I buy stuff?</b><br />
            There may or may not be a merch shop at a later date. We welcome polite suggestions.<br />
            Currently [2021] there is only <a href="https://www.smashwords.com/profile/view/CMWeller">Smashwords</a> and <a href="https://www.lulu.com/spotlight/KFZ">Lulu</a> where you can own a thing and also give us money.
          </p>
        </div>
        <div v-else-if="mode==='search'">
          <v-list-item
              v-for="(title, number) in searchResults"
              :key="number" @click.stop="gotoNumber(number)"
          >
            <v-list-item-content
            >
              <v-list-item-title>
                <v-icon left>mdi-file-document</v-icon>
                {{ title }}
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </div>
        <div v-else-if="mode==='story'">
          <div class="text-h4">
            {{story.title}}

            <v-btn icon class="mr-sm-1" @click.stop="favStory(number)">
              <v-icon :color="favColour(number)">{{ favIcon(number) }}</v-icon>
            </v-btn>
          </div>

          <VueDocPreview
              :value="story.prompt"
              class="text-h6"
              type="markdown"
          />

          <v-chip
              class="mr-1 pa-1"
              small
              v-for="tag in tags"
              :key="tag"
              label
          >
            {{ tag }}
          </v-chip>

          <VueDocPreview
              :value="story.content"
              class="body-1"
              type="markdown"
          />


        </div>
        <div v-else-if="mode==='thanks'">
          <!-- This is the bit where I thank all the patrons in descending order of donation value -->
          <h2>Many Gracious thanks to...</h2>
          <p><b>Primary Codination:</b> norganna<br />
             <b>Miminal Codination:</b> InterNutter<br />
             <b>Flights of Fantasy:</b> C. M. Weller
          </p>
          <h3>Lovely Patrons:</h3>
          <ul>
            <li><v-icon left>mdi-star</v-icon><i>Reckless Prudence</i>,</li>
            <li>Richard Morse,</li>
            <li>Kelda Choc,</li>
            <li>Wayne Roy,</li>
            <li>Emily Scribe Protra,</li>
            <li>Scott Haubert,</li>
            <li>Megan McCauley,</li>
            <li>Ran Akki,</li>
          </ul>
          <h3>...And You</h3>
        </div>
        <div v-else>
          <div class="text-h4">Welcome to Mobile Instants!</div>
          The buttons below will take you to a story.

        </div>
      </v-container>
    </v-main>

    <v-footer app>
      <v-col
          class="text-center"
          cols="12"
      >
        <v-btn
            :fab="$vuetify.breakpoint.smAndDown"
            :tile="$vuetify.breakpoint.mdAndUp"
            small color="primary" outlined
            class="mr-sm-1"
            @click.stop="navigate(-3)"
        >
          <v-icon>
            mdi-chevron-triple-left
          </v-icon>
          <span v-if="$vuetify.breakpoint.mdAndUp"> First</span>
        </v-btn>

        <v-btn
            :fab="$vuetify.breakpoint.smAndDown"
            :tile="$vuetify.breakpoint.mdAndUp"
            small color="primary" outlined
            class="mr-sm-1"
            @click.stop="navigate(-2)"
        >
          <v-icon>
            mdi-chevron-double-left
          </v-icon>
          <span v-if="$vuetify.breakpoint.mdAndUp"> -10</span>
        </v-btn>

        <v-btn
            :fab="$vuetify.breakpoint.smAndDown"
            :tile="$vuetify.breakpoint.mdAndUp"
            small color="primary" outlined
            class="mr-sm-1"
            @click.stop="navigate(-1)"
        >
          <v-icon>
            mdi-chevron-left
          </v-icon>
          <span v-if="$vuetify.breakpoint.mdAndUp"> Prev</span>
        </v-btn>

        <v-btn icon class="mr-sm-1" @click.stop="favStory(number)">
          <v-icon :color="favColour(number)">{{ favIcon(number) }}</v-icon>
        </v-btn>

        <div class="story-number" @click="perform('show-num-window')">
          {{number}}
        </div>

        <v-btn
            :fab="$vuetify.breakpoint.smAndDown"
            :tile="$vuetify.breakpoint.mdAndUp"
            small color="primary" outlined
            class="mr-sm-1"
            @click.stop="navigate(4)"
        >
          <v-icon>
            mdi-shuffle-variant
          </v-icon>
          <span v-if="$vuetify.breakpoint.mdAndUp"> Random</span>
        </v-btn>

        <v-btn
            :fab="$vuetify.breakpoint.smAndDown"
            :tile="$vuetify.breakpoint.mdAndUp"
            small color="primary" outlined
            class="mr-sm-1"
            @click.stop="navigate(1)"
        >
          <v-icon>
            mdi-chevron-right
          </v-icon>
          <span v-if="$vuetify.breakpoint.mdAndUp"> Next</span>
        </v-btn>

        <v-btn
            :fab="$vuetify.breakpoint.smAndDown"
            :tile="$vuetify.breakpoint.mdAndUp"
            small color="primary" outlined
            class="mr-sm-1"
            @click.stop="navigate(2)"
        >
          <v-icon>
            mdi-chevron-double-right
          </v-icon>
          <span v-if="$vuetify.breakpoint.mdAndUp"> +10</span>
        </v-btn>

        <v-btn
            :fab="$vuetify.breakpoint.smAndDown"
            :tile="$vuetify.breakpoint.mdAndUp"
            small color="primary" outlined
            class="mr-sm-1"
            @click.stop="navigate(3)"
        >
          <v-icon>
            mdi-chevron-triple-right
          </v-icon>
          <span v-if="$vuetify.breakpoint.mdAndUp"> Latest</span>
        </v-btn>


        <br />
        <small>&copy; 2013-2021 C. M. Weller, all rights reserved.</small>

        <!-- Ideal space for IP claim, donate option(s), share option(s), [add to faves if logged in] -->
      </v-col>
      <!-- -->
    </v-footer>

    <v-snackbar
        v-model="snackbar"
        multi-line top :timeout='6000' color="cyan darken-2"
    >
      {{ snacktext }}
    </v-snackbar>

    <v-dialog
        v-model="calendar"
        max-width="290"
    >
      <v-date-picker v-model="picker" @change="gotoDate()"></v-date-picker>
    </v-dialog>

    <v-dialog v-model="numselect" max-width="290">
      <v-card>
        <v-list-item two-line>
          <v-list-item-content>
            <div class="overline mb-4">Story number</div>
            <v-list-item>
              <v-text-field
                  v-model="storyNum"
                  :rules="storyNumRules"
                  :counter="4"
                  label="Story Number"
                  @keydown.enter="gotoNum(storyNum)"
                  @focus="$event.target.select()"
                  autofocus
                  required
              ></v-text-field>
            </v-list-item>
          </v-list-item-content>
        </v-list-item>
        <v-card-actions>
          <v-btn text color="primary" @click.stop="gotoNum(storyNum)">Go</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <v-dialog v-model="tagselect" max-width="290">
      <v-card>
        <v-list-item two-line>
          <v-list-item-content>
            <div class="overline mb-4">Search Tag</div>
            <v-list-item>
              <v-text-field
                  v-model="storyTag"
                  :rules="storyTagRules"
                  label="Story Tag"
                  @keydown.enter="searchTag(storyTag)"
                  required
              ></v-text-field>
            </v-list-item>
          </v-list-item-content>
        </v-list-item>
        <v-card-actions>
          <v-btn text color="primary" @click.stop="searchTag(storyTag)">Search</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

  </v-app>
</template>

<style>
.vm-markdown-html {
  padding-left: 0 !important;
}
.story-number {
  width: 3em;
  text-align: center;
  display: inline-block;
}
</style>

<script>
import VueDocPreview from 'vue-doc-preview';

let config = {
  apiURL: `${document.location.protocol}//${document.location.hostname}:3000`,
};

const startDate = new Date(2013,0,1, 0, 0, 0, 0);

function numberForDate(date) {
  const diff = date-startDate;
  let days = diff / 86400000;
  if (days > 365+31+28) days++;
  return (~~days)+1;
}

export default {
  name: 'App',

  components: {
    VueDocPreview,
  },

  data: () => ({
    mode: 'home',
    drawer: null,
    items: [
      // Nav by calendar
      // Nav by storyNum
      // Nav by tag
      // FAQ
      // Optional sign up/sign in noise
      {
        title: 'Search by Date',
        icon: 'mdi-calendar',
        action: 'show-calendar'
      },
      {
        title: 'Search by Number',
        icon: 'mdi-numeric',
        action: 'show-num-window'
      },
      {
        title: 'Search by Tag',
        icon: 'mdi-tag',
        action: 'show-tag-search'
      },
      {
        title: 'FAQ',
        icon: 'mdi-frequently-asked-questions',
        action: 'show-faq'
      },
      {
        title: 'Thanks',
        icon: 'mdi-emoticon-kiss',
        action: 'show-thanks'
      },
      {
        title: 'Donate Options',
        icon: 'mdi-cash-multiple',
        action: 'show-donates'
      },
      {
        title: 'Settings',
        icon: 'mdi-cog',
        signedIn: true
      },
      {
        title: 'Sign In',
        icon: 'mdi-account',
        action: 'sign-in',
        signedIn: false
      },
      {
        title: 'Register',
        icon: 'mdi-account-plus',
        action: 'show-register',
        signedIn: false
      },
      {
        title: 'Sign Out',
        icon: 'mdi-logout',
        action: 'sign-out',
        signedIn: true
      }
    ],
    account: null,
    number: 0,
    story: null,
    tags: [],
    snacktext: '',
    snackbar: false,
    calendar: false,
    picker: (new Date()).toISOString().split('T')[0],
    numselect: false,
    storyNum: 0,
    storyNumRules: [
      v => !!v || 'Number is required',
      v => v.length <= 4 || 'Number is too big',
      v => /^\d+/.test(v) || 'Text is not a number',
    ],
    tagselect: false,
    storyTag: '',
    storyTagRules: [
        v => !!v || 'Text field empty',
        v => v.length > 1 || 'Tag too short',
    ],
    searchResults: null,
    favourites: {},
  }),
  created() {
    fetch('config.json').then(async(res) => {
      try {
        config = await res.json();
      } catch (e) {
        return;
      }
    });
  },
  mounted() {
    const that = this;
    fetch(`${config.apiURL}/account`, {
      credentials: "include"
    }).then(async(res) => {
      try {
        const account = await res.json();
        if (account && account.signedIn) {
          that.account = account;
          that.loadFavourites();
        }
      } catch (e) {
        that.snacktext='Failed to decode account response.';
        that.snackbar=true;
      }
    }).catch(() => {
      that.snacktext='Error trying to fetch account.';
      that.snackbar=true;
    });
  },
  computed: {
    getItems() {
      const items=[];
      for (const item of this.items) {
        if (item.signedIn === true && this.account
            || item.signedIn === false && !this.account
            || item.signedIn === undefined) {
          items.push(item);
        }
      }
      return items;
    },

  },
  methods: {
    hamburger() {
      console.log('hamburger clicked')
      // I do believe this is where all the nav buttons mentioned above go?
      this.drawer = !this.drawer;

    },
    navigate(speed) {
      let number = 0;
      if (!this.number && speed !== -3 && speed !== 4) {
        number = 'last';
      } else {
        switch (speed) {
          case -3:
            number = 1;
            break;
          case -2:
            number = this.number - 10;
            if (number < 1) number = 1;
            break;
          case -1:
            number = this.number - 1;
            if (number < 1) number = 1;
            break;
          case 1:
            number = this.number + 1;
            break;
          case 2:
            number = this.number + 10;
            break;
          case 3:
            number = 'last';
            break;
          case 4:
            number = 'random';
            break;
        }
      }

      this.load(number);
    },
    load(number) {
      if (!number) {
        number = 'last';
      }
      const that = this;

      fetch(`${config.apiURL}/story/${number}`).then(async (res)=> {
        try {
          that.reset();
          that.story = await res.json();
          that.number = that.story.number;
          that.mode='story';
        } catch (e) {
          that.snacktext='Whoops! No story to be had.';
          that.snackbar=true;
        }
      }).catch (() => {
        that.snacktext='Whoops! Error fetching story.';
        that.snackbar=true;
      });
      fetch(`${config.apiURL}/tags/${number}`).then(async (res)=> {
        that.tags = await res.json();
      });

    },
    loadFavourites() {
      const that = this;
      fetch(`${config.apiURL}/favourites`, {
        credentials: "include"
      }).then(async(res) => {
        try {
          const faves = await res.json();
          if (faves) {
            const favourites = {};
            for (const fave of faves) {
              favourites[fave] = true;
            }
            that.favourites = favourites;
          }
        } catch (e) {
          that.snacktext='Failed to decode favourites response.';
          that.snackbar=true;
        }
      }).catch(() => {
        that.snacktext='Error trying to fetch favourites.';
        that.snackbar=true;
      });

    },
    signOut() {
      const that = this;
      fetch(`${config.apiURL}/sign-out`, {
        credentials: "include"
      }).then(() => {
        that.account = null;
      });
    },
    gotoDate() {
      this.calendar=false;
      const date=this.picker;
      const number = numberForDate(new Date(date));
      this.load(number);
    },
    gotoNum() {
      this.numselect=false;
      this.load(this.storyNum);
    },
    gotoNumber(number) {
      this.searchResults = null;
      this.load(number);
    },
    gotoURL(href) {
      window.open(href, '_blank');
    },
    gotoSignIn() {
      document.location = `${config.apiURL}/sign-in`;
    },
    searchTag(tag) {
      this.tagselect = false;
      const that = this;
      fetch(`${config.apiURL}/tag/${tag.toLowerCase()}`).then(async (res)=> {
        try {
          that.reset();
          that.searchResults = await res.json();
          that.mode = 'search';
        } catch (e) {
          that.snacktext = 'Whoops! No stories to be found.';
          that.snackbar = true;
        }
      }).catch (() => {
        that.snacktext = 'Whoops! Error fetching stories.';
        that.snackbar = true;
      });
    },
    reset() {
      this.searchResults = null;
      this.calendar = false;
      this.numselect = false;
      this.tagselect = false;
    },
    perform(action) {
      this.reset();
      switch (action) {
        case 'show-calendar':
          this.calendar = true;
          break;
        case 'show-num-window':
          this.numselect = true;
          break;
        case 'show-tag-search':
          this.tagselect = true;
          break;
        case 'show-faq':
          this.mode = 'faq';
          break;
        case 'show-donates':
          this.mode = 'donate';
          break;
        case 'sign-in':
          this.gotoSignIn();
          break;
        case 'sign-out':
          this.signOut();
          break;
        case 'show-thanks' :
          this.mode = 'thanks';
          break;
      }
    },
    favStory(number) {
      if (!this.account) {
        this.snacktext = 'Sorry, this app will not remember your favourites if you are not logged in. Please log in or create an account.'
        this.snackbar = true;
        return;
      }
      const set = !this.favourites[number];
      this.$set(this.favourites, number, set);
      fetch(`${config.apiURL}/favourite`, {
        method: 'POST',
        headers:  new Headers({
          'Content-Type': 'application/json; charset=utf-8'
        }),
        body: JSON.stringify({
          number,
          set,
        }),
        credentials: "include",
      });
      /*

      POST /favourite
      {
        "number": 1234,
        "set": true
      }

      + How do we tell it what story number we're adding / clearing this favourite from?
      + How do we tell it that we're ADDING or CLEARING?
      + Are we just sending an ADD / CLEARING one at a time?

       */


      // take number and add it to the database table of user favourites
    },
    favIcon(number) {
      if (this.favourites[number]) {
        return 'mdi-heart';
      }
      return 'mdi-heart-outline';
    },
    favColour(number) {
      if (this.favourites[number]) {
        return 'red';
      }
      return 'primary';
    },
  }
}
</script>
