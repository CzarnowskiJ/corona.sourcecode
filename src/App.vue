<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text"
        class="search-bar"
        placeholder="Search..."
        v-model="query"
        @keypress="fetchCovid"
        @keyup.enter="setQuery"
        />
      </div>
        <div class="welcome-wrap" v-if="typeof covid[0] === 'undefined' && setQ.length == 0">
          <div class="welcome-message">Covid-19 Confirmed Cases App</div>
          <div class="welcome-box">Use the search bar to find current data about Covid-19 cases in every counry in the world.</div>
        </div>
        <div class="response-wrap" v-if="covid.length === 0">
          <div class="response">{{setQ}}</div>
        </div>
        <div class="covid-wrap" v-if="typeof covid[0] != 'undefined'">
          <div class="location-box">
            <div class="location">{{covid[0]["country"]}}</div>
            <div class="date">{{date | formatDate}}</div>
          </div>


          <div class="covid-box">
            <div class="current">
              <p class="headline">Covid-19 cases:</p>
              <p>Confirmed: <span class="text">{{covid[0]["confirmed"]}}</span></p>
              <p>Critical: <span class="text1">{{covid[0]["critical"]}}</span></p>
              <p>Deaths: <span class="text2">{{covid[0]["deaths"]}}</span></p>
            </div>
            <div class="info">info via COVID-19 data by Gramzivi</div>
          </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {

  name: 'App',
    data () {
    return {
      api_key: 'a74a74a22msha0f89f1d257b488p12aa4bjsn1c1d1efab88d',
      url_base: 'https://covid-19-data.p.rapidapi.com/',
      query: '',
      setQ: '',
      covid:{},
      date: new Date()
    }
  },
  methods: {
    fetchCovid (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}/country?name=${this.query}`,
        {	"method": "GET",
          "headers": {
          "x-rapidapi-key": "4a74a74a22msha0f89f1d257b488p12aa4bjsn1c1d1efab88d",
          "x-rapidapi-host": "covid-19-data.p.rapidapi.com"}
        })
        .then(res => {return res.json();})
        .then(this.setResults)
      }
    },
    setResults (results) {
      this.covid = results
    },
    setQuery() {
     if (this.query.length == 0){
      this. setQ = 'You have to type the country name first.' }
     else {
      this.setQ = this.query + ' is not a coutnry. Please make sure that the name is correct.'
      }
    },
  }
}

import moment from 'moment'
import Vue from 'vue'

Vue.filter('formatDate', function(value) {
      if (value) {
        return moment(String(value)).format('DD MMMM YYYY')
      }
    })

</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Nunito:ital,wght@0,200;0,600;0,700;0,900;1,200;1,600;1,700&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Nunito', sans-serif;
}

#app {
  background-image: url('./assets/tlo.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.5s;
  align-items: center;
  justify-content: center;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(175, 175, 175, 0.507), rgba(172, 70, 70, 0.9));
  align-items: center;
  justify-content: center;
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: black;
  font-size: 15px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color:rgba(255, 255, 255, 0.411);
  border-radius:  19px 19px 19px 19px;
  box-shadow: 0px 5px 20px rgba(0, 1, 0, 0.50);
  transition: 0.5s;
  }

.search-box .search-bar:focus {
  background-color:rgba(255, 255, 255, 0.815);
  box-shadow: 0px 5px 10px rgba(0, 1, 0, 0.50);
  border-radius: 9px 9px 9px 9px;
}

.welcome-message{
  font-family: 'Bebas Neue', cursive;
  color: rgb(221, 111, 111);
  font-size: 40px;
  font-weight: 600;
  text-align: center;
  text-shadow: 2px 2px 2px rgba(0, 1, 0, 0.329);
}

.welcome-box {
 text-align: center;
}

.welcome-box {
  padding: 10px 25px;
  color: white;
  font-size: 150%;
  font-weight: 600;
  text-shadow:  2px 2px rgba(0, 1, 0, 0.50);
  background-color: rgba(255, 255, 255, 0.329);
  border-radius: 15px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 1, 0, 0.205);
}

.response-wrap .response {
  color: white;
  text-align: center;
  font-size: 18px;
  font-weight: 600;
  text-shadow: 2px 3px 5px rgba(0, 1, 0, 0.329);
}

.location-box {
  margin-top: 80px;
}

.location-box .location {
  color: white;
  font-size: 7vh;
  font-weight: 900;
  text-align: center;
  text-shadow: 2px 3px 5px rgba(0, 1, 0, 0.329);
}

.location-box .date {
  color: white;
  font-size: 25px;
  font-weight: 700;
  font-style: italic;
  text-align: center;
}

.covid-box {
 text-align: center;
}

.covid-box .current {
  display: inline-block;
  padding: 10px 25px;
  color: white;
  font-size: 150%;
  font-weight: 600;
  text-shadow:  2px 2px rgba(0, 1, 0, 0.50);
  background-color: rgba(255, 255, 255, 0.329);
  border-radius: 15px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 1, 0, 0.205);
}

.covid-box .current .headline {
  font-weight: 700;
  margin-bottom: 20px;
  }

.covid-box .current .text {
  font-weight: 700;
  text-shadow:  2px 2px rgba(0, 1, 0, 0.25);
  }

.covid-box .current .text1 {
  font-weight: 700;
  text-shadow:  2px 2px rgba(0, 1, 0, 0.25);
  color: rgb(240, 114, 114);
  }
.covid-box .current .text2 {
  font-weight: 700;
  text-shadow:  2px 2px rgba(0, 1, 0, 0.25);
  color: rgb(19, 19, 19);
}
.covid-box .info {
  color:rgba(255, 255, 255, 0.534);
  font-size: 15px;
  font-weight: 200;
  font-style: italic;
  text-shadow: 3px 2px rgba(0, 1, 0, 0.205);
}
</style>