<template>
  <div id="header">   
    <div class="Brand">{{ brand }}</div>
    <div class="Proprietor">{{ proprietor }}</div>
    <div class="Contact">
      <table>
          <tr v-for="contact_line in contact_lines" :key="contact_line"><td>{{ contact_line }}</td></tr>
      </table>
    </div>
  </div>
  <!-- <br class="clearboth">  -->
  <!-- <p>The desired date is {{ datetime }}. The desired locale is {{ locale }}.</p> -->
  <div class="DateTime">
    <DateTimeLocalized :locale="locale" :format="format"/>
    <!-- <DateTimeLocalized :datetime="datetime" :format="format"/> 
    <DateTimeLocalized :locale="locale" :format="format"/>
    <DateTimeLocalized :format="format"/> 
    <DateTimeLocalized/>
    <DateTimeLocalized :datetime="new Date(1969, 6, 20)" :format="format"/>
    <DateTimeLocalized :datetime="new Date(1969, 6, 20)" :locale="'de-DE'" :format="format"/> 
    <DateTimeLocalized :locale="'fr-FR'" :format="format"/>
    <DateTimeLocalized :datetime="new Date(1969, 6, 20)" :locale="'ar-SA'" :format="format"/>
    <DateTimeLocalized :locale="'ar-SA'" :format="format"/>
    <DateTimeLocalized :datetime="new Date(1969, 6, 20)" :locale="'xx-XX'" :format="format"/>
    <DateTimeLocalized :locale="'en-CA'" :format="'TimeDate'"/> -->
    <!-- <br class="clearboth"> -->
  </div>
</template>


<script>
import DateTimeLocalized from './DateTimeLocalized.vue';

export default {
  name: 'Title',
  components: { DateTimeLocalized },
  props: {
      brand: { type: String, required: true },
      proprietor: { type: String, required: true },
      contact_lines: { type: Array, required: false, default: () => ["Contact Data Pending"] }, //simple array
  },
  data() {
    return {
      // datetime: new Date(2020, 11, 31, 1, 2, 3),
      locale: "en-CA",
      format: "Date"      
    }
  },
 created()  {
    console.log("Created Title");
  } 
 }


</script>  

<style scoped>
@font-face {
    font-family: 'advent_probold';
    src: url('../assets/fonts/adventpro/adventpro-bold-webfont.woff2') format('woff2'),
         url('../assets/fonts/adventpro/adventpro-bold-webfont.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}
@font-face {
  font-family: 'amaranthbold_italic';
  src: url("../assets/fonts/amaranth/amaranth-bolditalic-webfont.woff2") format("woff2"), 
       url("../assets/fonts/amaranth/amaranth-bolditalic-webfont.woff") format("woff");
  font-weight: normal;
  font-style: normal;
}
@font-face {
  font-family: 'arsenalregular';
  src: url("../assets/fonts/arsenal/arsenal-regular-webfont.woff2") format("woff2"), 
       url("../assets/fonts/arsenal/arsenal-regular-webfont.woff") format("woff");
  font-weight: normal;
  font-style: normal;
}

#header {
	background: #753448 url("../assets/images/HeaderBackground.gif") repeat top left; 
	border: 0.75em solid white;
	box-shadow: 0em 0.2em 0.4em 0.1em #999; 
	border-radius: 0.1em;		
	overflow: hidden; 	
    display: grid;
    grid-column-gap: 20px;
    grid-template-columns: 50% 30% 20%;
}

.Brand {
  grid-column-start: 1;
  grid-column-end: 1;
  font-family: amaranthbold_italic, advent_probold, sans-serif;
  font-size: 5em;
  font-style: italic;  
  font-weight: bold; 
  text-align: center;
	color: white;
	background: transparent;
	text-shadow: 0em 0.1em 0.1em rgba(0,0,0,0.4),
             0em 0.2em 0.25em rgba(0,0,0,0.1),
             0em 0.3em 0.4em rgba(0,0,0,0.1); 
}
.Proprietor {
	grid-column-start: 2;
  grid-column-end: 2;
  font-family: "Times Roman", serif;
  font-size: 2.5em;
  font-style: italic;
  font-weight: bold;
	color: gold;
	background: transparent;
	text-shadow: 0em 0.1em 0.1em rgba(0,0,0,0.4),
             0em 0.2em 0.25em rgba(0,0,0,0.1),
             0em 0.3em 0.4em rgba(0,0,0,0.1); 	
	margin: 0.5em 0 0 0;	
}
.Contact {
	grid-column-start: 3;
  grid-column-end: 3;
  font-family: arsenalregular, sans-serif;
	font-size: 0.8em;
	font-weight: bold;
  text-align: left;
	color: aliceblue;
	background: transparent;
}
.DateTime {
  text-align: left;
}
td {
  line-height: 12px;
}
.clearboth {
	clear: both;
	height: 2em;
	}
</style>
