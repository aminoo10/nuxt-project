<template>
  <div class="rec-container">
    <h1 class="mt-5">Personal Recommendations: </h1>
    <h6>From the Website's Developer</h6>
    <p>Here are some of my biggest recommedations that I personally really enjoy and suggest others to check out! </p>
    <hr>
    <h3 class="mb-5">Anime:</h3>
      <div class="animes">
        <Card v-for="anime of animeTitles" :key="anime.mal_id" :item="anime" :manga="false"/>
        <!-- <p> {{anime.description}} </p> -->
      </div>
    <hr>
    <h3 class="mb-5">Manga:</h3>
    <div class="mangas mb-5">
      <Card v-for="manga of mangaTitles" :key="manga.mal_id" :item="manga" :manga="true"/>
      <!-- <p> {{manga.description}} </p> -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return{
      //I was going to include my own comments on why I enjoy the choices I picked, but I guess if a view were curious, they'd always just look at the synopsis of the anime. (plus I was having some issues lining up the text next to the info-card )
      animeTitles: [
        {title: 'Redline', mal_id:6675, image_url: 'https://cdn.myanimelist.net/images/anime/12/28553.jpg', description: 'Amazing movie with incredible animation, I\'ve watched it multiple times and never get tired of it! From one of the best animation studios in the industry, Madhouse!'},
        {title: 'Gyakkyou Burai Kaiji: Ultimate Survivor', mal_id: 3002, image_url: 'https://cdn.myanimelist.net/images/anime/12/80032.jpg', description: 'Despair, Excitement, Tension! Lots of people are put off by Kaiji\'s art style, but the author\'s signature look really makes this image of this terrible gambling underworld dark and bleak, also amazing animation from the incredible Madhouse!'},
        {title: 'Neon Genesis Evangelion', mal_id: 30, image_url: 'https://cdn.myanimelist.net/images/anime/1314/108941.jpg', description: 'A true classic of 90s anime televsion and a revolutionary product of its time for its unique story, and deep psychological analysis of its characters, it went on to cement hideaki anno\'s career and start one of the biggest anime franchises in japan, the money made from this franchise and products figures out to a large portion of japan\'s economy!' },
        {title: 'Porco Rosso', mal_id: 416, image_url: 'https://cdn.myanimelist.net/images/anime/6/2878.jpg', description: 'My favorite Ghibli movie, nothing too complex, nothing much at stake, just a fun adventure and story through 1930s Italy. It\'s been said that the main character is something of a self-insert of the director, which I find kind of amusing'},
        {title: 'Perfect Blue', mal_id: 437, image_url: 'https://cdn.myanimelist.net/images/anime/11/79127.jpg', description: 'Another from Madhouse! One of Satoshi Kon\'s first cinema features which includes high suspense, mystery, and murder. A lot of Satoshi Kon\'s work is mostly rooted in reality, with nothing that gets too fantastic. It is a great psychological drama and the inspiration for the movie "Black Swan". Much of Satoshi Kon\'s work equates and even exceeds the quality of this movie, it\'s such a devastaing loss to have lost this man to cancer back in 2010' }
      ],
      mangaTitles: [
        {title: 'One Piece', mal_id: 13, image_url: 'https://cdn.myanimelist.net/images/manga/3/55539.jpg', description: 'One of the biggest ongoing manga franchises to date, even after 1000 chapters (holy crap!) the story still remains fresh and exciting, and there is still so much left to go!!! Has an Anime adpation that is also good' },
        {title: 'Berserk', mal_id: 2 , image_url: 'https://cdn.myanimelist.net/images/manga/1/157897.jpg', description: 'A classic manga series, known as "The Strongest Fantasy Comic" in publication, a great epic of a man\'s path through misery, and struggle, and a wonderful world built within it. Unfortunately often goes on hiatus for long periods of time due to the author\'s growing interest in other hobbies. Fans of the Game of Thrones will enjoy this one'},
        {title: 'Dorohedoro', mal_id: 1133 , image_url: 'https://cdn.myanimelist.net/images/manga/2/143111.jpg', description: 'A little more recent title, this one had been in publication for about 18 years, being updated monthly. The creator is a fan of western horror movies so there is a lot of influence from it in there, but for the most part I just like the world and the art a lot! Got an anime adaption recently on Netflix!'},
        {title: 'One Punch-Man', mal_id: 44347 , image_url: 'https://cdn.myanimelist.net/images/manga/3/80661.jpg', description: 'Starting as a webcomic made by the writer ONE, the artist Yusuke Murata fell deathly ill, fearing that if he died, he would miss the chance to be able to work with ONE. Fortunately he recovered and he has been working diligently and effortlessly on recreating ONE\'s masterpiece story and representing it in the best way he can, often scrapping pages and chapters and redrawing them wholesale after magazine publication. Also had a very successful Anime! With the first season by Madhouse!!! (you can skip season 2)'},
        {title: 'Fist of the North Star', mal_id: 1149, image_url: 'https://cdn.myanimelist.net/images/manga/3/830.jpg', description: 'One of the greatest mangas ever created, incredibly masterful storytelling and art, I couldn\'t believe this was a weekly manga when I read this, purely insane dedication and effort has gone through this masterful piece of storytelling.'}
      ],
    }
  },
    head() {
    return {
      title: 'Recommendations',
      meta: [
        {
          hid: 'A listing of titles recommended by the webmaster',
        }
       ]
    }
  }
}
</script>

<style lang="scss" scoped>

.rec-container {
  min-height: 80vh;
  display: flex;
  flex-direction: column;
  text-align: center;
}

.animes, .mangas {
  display: flex;
  flex-wrap: wrap;
  flex-direction: center;
  justify-content: center;
  align-content: space-between;
  text-align: center;
}

h3 {
  text-decoration: underline;
}



</style>