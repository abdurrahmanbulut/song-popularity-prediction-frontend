<template>
  <div v-if="playSong">
  
    <div
      class="spotifyCardContainer"
    >
      <div
      class="spotifyCardSubContainer"
      >
        <iframe
          id="spotify-music"
          v-bind:src="this.newUrl"
          width="90%"
          height="80px"
          allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
          loading="lazy"
        ></iframe>
        <div
        class="spotifyCardImgContainer"
         
        >
          <img
            src="../assets/img/icons/close-icon.svg"
            @click="changeSpotifyCard()"
            style="cursor: pointer; width: 2rem"
            alt=""
          />
        </div>
      </div>

      <div class="song-info-card">
        <div class="song-info-subcard">
          <table class="feature-table" v-if="info">
            <tr>
              <th>acousticness</th>
              <td>{{ this.audio_features.acousticness }}</td>
            </tr>

            <tr>
              <th>danceability</th>
              <td>{{ this.audio_features.danceability }}</td>
            </tr>

            <tr>
              <th>duration(ms)</th>
              <td>{{ this.audio_features.duration_ms }}</td>
            </tr>
            <tr>
              <th>energy</th>
              <td>{{ this.audio_features.energy }}</td>
            </tr>
            <tr>
              <th>instrumentalness</th>
              <td>{{ this.audio_features.instrumentalness }}</td>
            </tr>
            <tr>
              <th>liveness</th>
              <td>{{ this.audio_features.liveness }}</td>
            </tr>
            <tr>
              <th>loudness</th>
              <td>{{ this.audio_features.loudness }}</td>
            </tr>
            <tr>
              <th>mode</th>
              <td>{{ this.audio_features.mode }}</td>
            </tr>
            <tr>
              <th>speechiness</th>
              <td>{{ this.audio_features.speechiness }}</td>
            </tr>
            <tr>
              <th>tempo</th>
              <td>{{ this.audio_features.tempo }}</td>
            </tr>
            <tr>
              <th>time signature</th>
              <td>{{ this.audio_features.time_signature }}</td>
            </tr>
            <tr>
              <th>valence</th>
              <td>{{ this.audio_features.valence }}</td>
            </tr>
            <tr>
              <th>explicit</th>
              <td>{{ this.album_features.explicit }}</td>
            </tr>
            <tr>
              <th>valence</th>
              <td>{{ this.audio_features.valence }}</td>
            </tr>
            <tr>
              <th>release date</th>
              <td>
                {{ this.album_features.album.release_date.substring(0, 4) }}
              </td>
            </tr>
          </table>


          <table class="feature-info-table" v-else>
            <tr>
              <th>acousticness</th>
              <td>A confidence measure from 0.0 to 1.0 of whether the track is acoustic. 1.0 represents high confidence the track is acoustic.</td>
            </tr>

            <tr>
              <th>danceability</th>
              <td>Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable.</td>
            </tr>

            <tr>
              <th>duration(ms)</th>
              <td>The duration of the track in milliseconds.</td>
            </tr>
            <tr>
              <th>energy</th>
              <td>Energy is a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity. Typically, energetic tracks feel fast, loud, and noisy. For example, death metal has high energy, while a Bach prelude scores low on the scale. Perceptual features contributing to this attribute include dynamic range, perceived loudness, timbre, onset rate, and general entropy.</td>
            </tr>
            <tr>
              <th>instrumentalness</th>
              <td>Predicts whether a track contains no vocals. "Ooh" and "aah" sounds are treated as instrumental in this context. Rap or spoken word tracks are clearly "vocal". The closer the instrumentalness value is to 1.0, the greater likelihood the track contains no vocal content. Values above 0.5 are intended to represent instrumental tracks, but confidence is higher as the value approaches 1.0.</td>
            </tr>
            <tr>
              <th>liveness</th>
              <td>Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that the track was performed live. A value above 0.8 provides strong likelihood that the track is live.</td>
            </tr>
            <tr>
              <th>loudness</th>
              <td>The overall loudness of a track in decibels (dB). Loudness values are averaged across the entire track and are useful for comparing relative loudness of tracks. Loudness is the quality of a sound that is the primary psychological correlate of physical strength (amplitude). Values typically range between -60 and 0 db.</td>
            </tr>
            <tr>
              <th>mode</th>
              <td>Mode indicates the modality (major or minor) of a track, the type of scale from which its melodic content is derived. Major is represented by 1 and minor is 0.</td>
            </tr>
            <tr>
              <th>speechiness</th>
              <td>Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value. Values above 0.66 describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. Values below 0.33 most likely represent music and other non-speech-like tracks.</td>
            </tr>
            <tr>
              <th>tempo</th>
              <td>The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or pace of a given piece and derives directly from the average beat duration.</td>
            </tr>
            <tr>
              <th>time signature</th>
              <td>An estimated time signature. The time signature (meter) is a notational convention to specify how many beats are in each bar (or measure). The time signature ranges from 3 to 7 indicating time signatures of "3/4", to "7/4".</td>
            </tr>
            <tr>
              <th>valence</th>
              <td>A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry).</td>
            </tr>
            <tr>
              <th>explicit</th>
              <td>if the track is rated as explicit.</td>
            </tr>
            <tr>
              <th>valence</th>
              <td>A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry).</td>
            </tr>
            <tr>
              <th>release date</th>
              <td>
                album release date
              </td>
            </tr>
          </table>
          
          <button class="btn-style" @click="changeInfo">
            <span v-if="this.info==true">see descriptions of features</span>
            <span v-if="this.info==false">Close descriptions of features</span>

          </button>
        </div>

        <div
          class="popularityCardContainer"
        >
          <br />
          <br />
          <label for="actual-popularity">Actual popularity</label> <br />
          <div class="animated-progress progress-white" :style="cssProps">
            <span class="actual" style="color: black">
              {{ this.actual_popularity }}%</span
            >
          </div>
          <br />
          <br />

          <label for="predicted-popularity">Predicted popularity</label> <br />
          <div class="animated-progress progress-white" :style="cssProps">
            
            <span v-if="this.predicted_popularity !== 0" class="predicted" style="color: black">
  
              {{ this.predicted_popularity }}%</span
            >
          </div>
          <span v-if="this.predicted_popularity === 0" style="margin-top:1rem">
              See the predicted value by pressing the predict button.
          </span>

          <br />
          <br />

          <div
          class="yearInputContainer"
        
          >
            <div style="width: 50%">
              <input
              class="yearInput"
                
                type="number"
                min="1920"
                max="2022"
                step="1"
                :value="this.year_of_song"
                @input="event => this.year_of_song = event.target.value"
                placeholder="year: yyyy"
              />
            </div>
            <div style="width: 30%">
              <button @click="predict" class="btn-style-predict">Predict</button>
            </div>
          </div>
          <span class="buttonInfo" >Change the song's release year and see its estimated popularity if the Song was released in the year you entered.</span>
        </div>
      </div>
    </div>
  </div>

  <div v-else-if="!playSong" class="spotify-card" @click="handleCardClick">
    <div class="spotify-card__picture">
      <img
        style="border-radius: 10%; height: 100%"
        :src="imageURL"
        alt="placeholder"
      />
    </div>

    <div class="spotify-card__info" style="padding: 1rem">
      <span class="spotify-card__title">{{ cardTitle }}</span>
      <span class="spotify-card__subtitle">{{ cardSubtitle }}</span>
    </div>
    <div class="test-train-card">
      <span style="background-color: green; height: 100%; width:100%;" v-if="this.cardInfo.db_status==1">Test</span>
      <span style="background-color: red; height: 100%;width:100%;"  v-if="this.cardInfo.db_status==0">Train</span>
      <span style="background-color: grey; height: 100%;width:100%;"  v-if="this.cardInfo.db_status==2">Not in the Dataset</span>
    </div>
  </div>
</template>


<script >
import { mapActions } from 'vuex';
import axios from 'axios';
import * as tf from '@tensorflow/tfjs';

export default {
  props: {
    cardInfo: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      cardType: this.cardInfo.type,
      cardTitle: this.cardInfo.name,
      playSong: false,
      newUrl: '',
      actual_popularity: 0,
      predicted_popularity: 0,
      posts: [],
      audio_features: {},
      album_features: {},
      year_of_song: 0,
      modelReady: false,
      predictedValue: 'click',
      valueToPredict: '',
      info: true,
      useEnsemble: true,
    };
  },
  
  mounted() {
    let that = this;
    async function loadModel() {
      
      that.model1 = await tf.loadLayersModel(
        'https://raw.githubusercontent.com/abdurrahmanbulut/song-popularity-prediction-web/redirect/src/assets/model/model_1980/model.json'
      );

      that.model2 = await tf.loadLayersModel(
        'https://raw.githubusercontent.com/abdurrahmanbulut/song-popularity-prediction-web/redirect/src/assets/model/model_1990/model.json'
      );

      that.model3 = await tf.loadLayersModel(
        'https://raw.githubusercontent.com/abdurrahmanbulut/song-popularity-prediction-web/redirect/src/assets/model/model_2000/model.json'
      );
      that.model4 = await tf.loadLayersModel(
        'https://raw.githubusercontent.com/abdurrahmanbulut/song-popularity-prediction-web/redirect/src/assets/model/model_2010/model.json'
      );
    }
    loadModel();
  },

  methods: {
    ...mapActions(['diplayToaster']),
    handleCardClick() {
      console.log('vard info', this.cardInfo);
      this.actual_popularity = this.cardInfo.popularity;
      if (this.cardInfo.type == 'track') {
        const temp = this.cardInfo.external_urls.spotify.split('com/');
        this.newUrl = temp[0] + 'com/embed/' + temp[1];
        this.playSong = true;
      }

      this.getPosts(this.cardInfo);
      this.album_features = this.cardInfo;
      this.year_of_song = +this.album_features.album.release_date.substring(
        0,
        4
      );
    },
    predictValue(values) {
    
      if(this.year_of_song < 1990){
         const prediction = this.model1.predict(values);
         return prediction;
      }
      else if(this.year_of_song < 2000){
         const prediction = this.model2.predict(values);
         return prediction;
      }
      else if(this.year_of_song < 2010){
         const prediction = this.model3.predict(values);
         return prediction;
      }
      else{
         const prediction = this.model4.predict(values);
         return prediction;
      }

    },
    predict() {
      
       // Create one dimensional array
      var input_arr = [[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1]]

      input_arr[0][0]  = this.album_features.explicit === false ? 0 : 1;
      input_arr[0][1]  = this.audio_features.danceability;
      input_arr[0][2]  = this.audio_features.energy;
      input_arr[0][3]  = this.audio_features.key;
      input_arr[0][4]  = this.audio_features.loudness;
      input_arr[0][5]  = this.audio_features.mode;
      input_arr[0][6]  = this.audio_features.speechiness;
      input_arr[0][7]  = this.audio_features.acousticness;
      input_arr[0][8]  = this.audio_features.instrumentalness;
      input_arr[0][9] = this.audio_features.liveness;
      input_arr[0][10] = this.audio_features.valence;
      input_arr[0][11] = this.audio_features.tempo;
      input_arr[0][12] = this.audio_features.time_signature;
      input_arr[0][13]  = this.audio_features.duration_ms / 1000.0;


      console.log("song", input_arr);

      input_arr[0] = this.standardizeArray(input_arr[0]);
      console.log("aa", input_arr);
      const x_test = tf.tensor2d(input_arr, [1, input_arr[0].length]);


      // if(this.useEnsemble == true){
      //   this.predicted_popularity = this.predictEnsemble(input_arr[0]);
      // }
      // else{
        this.predicted_popularity = this.predictValue(x_test);
        console.log("asd",this.predictValue(x_test));
        this.predicted_popularity.print();
        const tensorData = this.predicted_popularity.dataSync();
        
        this.predicted_popularity = tensorData[0];

        this.predicted_popularity = Math.round( this.predicted_popularity);
      //}
    

    },
    standardizeArray(arr) {

        // Find the minimum and maximum values in the array
        let minVal = -30;
        let maxVal = 800;
        // Create a new array to store the scaled values
        let scaledArr = arr.map(val => (val - minVal) / (maxVal - minVal));
        return scaledArr;
    },
    changeInfo() {
      this.info = !this.info;
    },
    getPosts(cardinfo) {
      axios({
        method: 'get',
        url: 'https://api.spotify.com/v1/audio-features?ids=' + cardinfo.id,
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json',
          Authorization:
            'Bearer ' + localStorage.getItem('spotify-access-token'),
        },
      }).then((response) => {
        this.audio_features = response.data.audio_features[0];
        console.log('audio', this.audio_features);
      });
    },
    //  predictEnsemble(values) {
    //    let data = {
    //     features: values
    //   }

    //   // Send a post request to the server
    //   axios.post('http://127.0.0.1:5000/predict', data)
    //     .then(response => {
    //       // Update the prediction data with the response
    //       this.prediction = response.data.prediction
    //     })
    //     .catch(error => {
    //       console.log(error)
    //     })
    // },

    changeSpotifyCard() {
      console.log(this.playSong);
      this.playSong = false;
      console.log(this.playSong);
    },
  },
  computed: {
    imageURL() {
      return (
        (this.cardType === 'track'
          ? this.cardInfo.album?.images[1]?.url
          : this.cardInfo.images[1]?.url) ||
        require('../assets/img/img-placeholder.jpg')
      );
    },
    cardSubtitle() {
      let subtitleText = '';
      if (this.cardType == 'track') {
        subtitleText = this.cardInfo.artists
          .map((artist) => artist.name)
          .join(', ');
      }
      return subtitleText;
    },
    cssProps() {
      return {
        '--progress-white-actual': this.actual_popularity + '%',
        '--progress-white-predicted': this.predicted_popularity + '%',
      };
    },
  },
};
</script>

<style lang="scss" scoped>
.spotify-card {
  border: 1px dotted #000000;
  cursor: pointer;
  width: 100%;
  height: 100px;

  display: grid;
  grid-template-columns: 100px auto 100px;
  border-radius: 0.9rem;

  transition: background-color 0.3s ease;
  .test-train-card{
    width:100px; height:100%;
    border-radius: 0.9rem;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    span{
      display: flex;
    justify-content: center;
    align-items: center;
      border-radius: 0.9rem;

    }

  }
  &:hover {
    background-color: grey;
    border-radius: 0.9rem;
  }

  &__picture {
    width: 100%;
    height: 100%;
    overflow: hidden;

    img {
      display: block;
      height: 100%;
      object-fit: cover;
    }

    &--round img {
      clip-path: circle(40% at center);
    }
  }

  &__info {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding: 10px 20px;
    overflow: hidden;

    span {
      // display: inline-block;
      width: calc(100%);
      text-align: left;
      white-space: nowrap;
      text-overflow: ellipsis;
      overflow: hidden;
    }
  }

  &__title {
    font-weight: bold;
    font-size: 1.1rem;
    margin-bottom: 0.3rem;
  }

  &__subtitle {
    font-weight: 300;
    font-style: italic;
    font-size: 0.8rem;
    color: $color-spotify-light-grey;
  }
}
.feature-table {
  width: 100%;
  height: 100%;
  margin-top: 2rem;
  th {
    text-align: start;
    border: 1px solid  #961c96;
    vertical-align: middle;
    padding-left: 5px;

  }
  tr {
    line-height: 24px;
  }
  tr:nth-child(even) {
    background-color: #d472aa;
  }
  td {
    vertical-align: middle;
    padding-left: 5px;
    border: 1px solid #961c96;
      
  }
 
}

.feature-info-table{
   width: 100%;
    height: 100%;
    margin-top: 2rem;
  th {
    text-align: start;
    border: 2px dotted #961c96;
    vertical-align: middle;
    width: 35%;
    padding-left: 5px;
  }
  tr {
    line-height: 24px;
  }
  tr:nth-child(even) {
    
}
  td {
    vertical-align: middle;
    border: 2px dotted #961c96;
    padding: 4px 0px 5px 4px;
  }

}
.song-info-card {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  margin-bottom: 3rem;
  .song-info-subcard {
    width: 40%;
  }
}
@media only screen and (min-width: map-get($breakpoints, 'lg')) {
}
@media only screen and (max-width: map-get($breakpoints, 'md')) {
  .song-info-card {
    flex-direction: column;
  }
  iframe {
    padding-right: 3rem;
  }
}
@media only screen and (max-width: map-get($breakpoints, 'sm')) {
  .song-info-card {
    flex-direction: column;
    .song-info-subcard {
      width: 90%;
    }
  }
}
@media only screen and (min-width: 0px) {
  .result-style {
    width: 90%;
  }
}
.animated-progress {
  width: 70%;
  height: 30px;
  border-radius: 8px;

  border: 1px solid rgb(189, 113, 113);
  position: relative;
}

.animated-progress .actual {
  height: 100%;
  display: block;
  width: var(--progress-white-actual);
  color: rgb(255, 251, 251);
  line-height: 30px;
  position: absolute;
  text-align: end;
  padding-right: 5px;
  border-radius: 8px 8px 8px 8px;
}
.animated-progress .predicted {
  height: 100%;
  display: block;
  width: var(--progress-white-predicted);
  color: rgb(255, 251, 251);
  line-height: 30px;
  position: absolute;
  text-align: end;
  border-radius: 8px 8px 8px 8px;
}

.progress-white span {
  background-color: rgb(255, 251, 251);
}
.btn-style {
  width: 100%;
  margin-top: 1rem;
  height: 2rem;
  border-radius: 8px;
  border: none;
}
.btn-style-predict{
  width: 100%;
  height: 2rem;
  border-radius: 8px;
  border: none;
}
.spotifyCardContainer{
    width: 100%;
    min-height: 25rem;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
.spotifyCardSubContainer{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.spotifyCardImgContainer{
  width: 10%;
            display: flex;
            justify-content: center;
            align-items: center;
}
.popularityCardContainer{
  width:100%; text-align:center; display:flex; flex-direction:column; align-items:center;
}
.yearInputContainer{
 width: 70%;
              height: 30px;
              border-radius: 5px;
              display: flex;
              justify-content: space-between;
}
.yearInput{
 width: 100%;
                  height: 100%;
                  border-radius: 8px;
                  border: none;
                  padding: 5px;
}
.buttonInfo{
  width:70%; margin-top: 1rem; padding:3px; line-height: 1.4rem; font-family: 'IBM Plex Serif', serif;
}
</style>