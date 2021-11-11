<template>

<head>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>

<body >

    <div class="wrapeer">

      <div class="menu-bar">
        <span class="menu-left-btn" @click="showingPage = 'calendar'"><i class="material-icons callendar" style="font-size:125%; margin-right:10px; ">insert_invitation</i></span>
        
        <span class="menu-right-btn material-icons" @click="showingPage = 'input'">create</span>
        <br><br>
        <span class="menu-left-btn" style="color:white;  margin-top:-10px; font-size:150%">日記</span>
        
      </div>

      <div class="selected-page" style="margin-top:80px">

        <div v-if="showingPage === 'input'" >
          <h2>HOW ARE YOU?</h2>

          <div class="mood-btn" style="text-align: justify;
      text-justify: inter-word;">
            <i class="material-icons callendar" style="font-size:125%; margin-right:10px; ">insert_invitation</i><select id="pet-select" v-model="selectingNum" style="font-size:110%; margin-right:60px">
              <option :value="6">{{DateList[6]}}</option>
              <option :value="5">{{DateList[5]}}</option>
              <option :value="4">{{DateList[4]}}</option>
              <option :value="3">{{DateList[3]}}</option>
              <option :value="2">{{DateList[2]}}</option>
              <option :value="1">{{DateList[1]}}</option>
              <option :value="0">{{DateList[0]}}</option>
            </select>
            <transition name="slide-fade">
                <i class="material-icons mood-btn " v-if="showingTextarea" v-bind:style="{ color: moodColor}" style="margin-left:-40px; position:fixed; font-size:30px" @click="showingTextarea = false">{{moodText}}</i>
            </transition>
          </div>

          <!-- <span>{{DateList}}</span> -->

          <br><br>
          <transition name="slide-fade">
            <div class="selecting-mood"  v-if="!showingTextarea">
              <i class="material-icons mood-btn " style="color:DarkBlue;  font-size:36px" @click="moodNum=1">sentiment_very_dissatisfied</i>
              <i class="material-icons mood-btn " style="color:CornflowerBlue;  font-size:36px" @click="moodNum=2">sentiment_dissatisfied</i>
              <i class="material-icons mood-btn;" style="font-size:36px; color:Seagreen" @click="moodNum=3">sentiment_neutral</i>
              <i class="material-icons mood-btn" style="color:Coral;  font-size:36px" @click="moodNum=4">sentiment_satisfied</i>
              <i class="material-icons mood-btn " style="color:#ff1919;  font-size:36px" @click="moodNum=5">sentiment_very_satisfied</i>
              <!-- rgb(255, 99, 71) -->
            </div>
          
          </transition>
          


          <div  class="textarea">
            <transition name="slide-fade">
              <div style="" class="topBar" v-if="showingTextarea">
            
                <!-- <span style="float:left; ">Length: {{contentLength}}</span> -->
                <button style="float:right;" class="button1 button" @click="sendData()">Send</button>
                

                <textarea name="" id="" cols="35" rows="20" v-model="actualContent" v-if="showingTextarea" style="margin-top:10px; font-size: 20px;"></textarea>

              </div>

              <!-- <div>
                
              </div> -->
            
            </transition>
          </div>

          <!-- <button @click="showingPage = 'main'"></button> -->
        </div>

        <div v-if="showingPage === 'editing'" >
          <h2>HOW ARE YOU?</h2>

          <div class="mood-btn" style="text-align: justify;
      text-justify: inter-word;">
            <i class="material-icons callendar" style="font-size:125%; margin-right:10px; ">insert_invitation</i>
            <strong>{{editing.year}}/{{editing.month}}/{{editing.date}} {{editing.yoobi}}</strong>
            <transition name="slide-fade">
                <i class="material-icons mood-btn " v-if="showingTextarea" v-bind:style="{ color: moodColor}" style="position:fixed; font-size:30px" @click="showingTextarea = false">{{moodText}}</i>
            </transition>
          </div>

          <!-- <span>{{DateList}}</span> -->

          <br><br>
          <transition name="slide-fade">
            <div class="selecting-mood"  v-if="!showingTextarea">
              <i class="material-icons mood-btn " style="color:DarkBlue;  font-size:36px" @click="moodNum = 1; editing.mood=1; showingTextarea = true">sentiment_very_dissatisfied</i>
              <i class="material-icons mood-btn " style="color:CornflowerBlue;  font-size:36px" @click="moodNum = 2;editing.mood=2; showingTextarea = true ">sentiment_dissatisfied</i>
              <i class="material-icons mood-btn;" style="font-size:36px; color:Seagreen" @click="moodNum = 3;editing.mood=3; showingTextarea = true">sentiment_neutral</i>
              <i class="material-icons mood-btn" style="color:Coral;  font-size:36px" @click="moodNum = 4;editing.mood=4; showingTextarea = true">sentiment_satisfied</i>
              <i class="material-icons mood-btn " style="color:#ff1919;  font-size:36px" @click="moodNum = 5;editing.mood=5; showingTextarea = true">sentiment_very_satisfied</i>
              <!-- rgb(255, 99, 71) -->
            </div>
          
          </transition>
          


          <div  class="textarea">
            <transition name="slide-fade">
              <div style="" class="topBar" v-if="showingTextarea">
            
                <!-- <span style="float:left; ">Length: {{contentLength}}</span> -->
                <button style="float:right;" class="button1 button" @click="updateData()">Update</button>
                

                <textarea name="" id="" cols="35" rows="20" v-model="editing.content" v-if="showingTextarea" style="margin-top:10px"></textarea>

              </div>

              <!-- <div>
                
              </div> -->
            
            </transition>
          </div>

          <!-- <button @click="showingPage = 'main'"></button> -->
        </div>

        <div v-if="showingPage === 'calendar' " >

          <div v-if="!showingCal" >
            <h2>Not having data yet</h2>
          </div>

          <div v-else>
            <div>
              <br>
              <div style="margin-top:-15px; margin-bottom:-10px">
                <input type="num" v-model="selectingYear" style="width: 10%;"> year
                &nbsp;
                <input type="num" v-model="showingMonthlyCount" style="width: 10%;"> month
                <button @click="setCalendar()">Update</button>

              </div>
              
    
              <div class="calendar-container">
                
          
                <header @touchstart="tStart($event)" @touchend="tEnd($event)" >
          
                  <div class="month">{{showingMonth}}</div>
                  <div class="year" style="marginTop:10px">{{showingYear}}</div>
          
                </header>
          
                <table class="calendar">
          
                  <thead>
          
                    <tr>
          
                      <td>Mon</td>
                      <td>Tue</td>
                      <td>Wed</td>
                      <td>Thu</td>
                      <td>Fri</td>
                      <td>Sat</td>
                      <td>Sun</td>
          
                    </tr>
          
                  </thead>
          
                  <tbody>
          
                    <tr>
                      <template v-for="(day, i) in showingCal" :key="i">
                        <td v-if="i<7 && (!dataList[showingYear][showingMonthlyCount][day.date] || day.additional) " :class="[day.additional ? 'prev-month' : '' ]"
                        class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>

                        <td v-if="i<7 && dataList[showingYear][showingMonthlyCount][day.date] && !day.additional" :class="[day.additional ? 'prev-month' : '' ]"
                        :style="{backgroundColor: moodStyle[dataList[showingYear][showingMonthlyCount][day.date].mood], color: textColor[dataList[showingYear][showingMonthlyCount][day.date].mood]}" class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>
                      </template>
                    </tr>

                    <tr>
                      <template v-for="(day, i) in showingCal" :key="i" >

                        <td v-if="(i >6 &&i<14) && (!dataList[showingYear][showingMonthlyCount][day.date] || day.additional) " :class="[day.additional ? 'prev-month' : '' ]"
                        class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>

                        <td v-if="(i >6 &&i<14) && dataList[showingYear][showingMonthlyCount][day.date] && !day.additional" :class="[day.additional ? 'prev-month' : '' ]"
                        :style="{backgroundColor: moodStyle[dataList[showingYear][showingMonthlyCount][day.date].mood], color: textColor[dataList[showingYear][showingMonthlyCount][day.date].mood]}" class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>
                      </template>
                    </tr>

                    <tr>
                      <template v-for="(day, i) in showingCal" :key="i" >

                        <td v-if="(i >13 &&i<21) && (!dataList[showingYear][showingMonthlyCount][day.date] || day.additional) " :class="[day.additional ? 'prev-month' : '' ]"
                        class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>

                        <td v-if="(i > 13&&i<21) && dataList[showingYear][showingMonthlyCount][day.date] && !day.additional" :class="[day.additional ? 'prev-month' : '' ]"
                        :style="{backgroundColor: moodStyle[dataList[showingYear][showingMonthlyCount][day.date].mood], color: textColor[dataList[showingYear][showingMonthlyCount][day.date].mood]}" class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>

                        
                      </template>
                    </tr>

                    <tr>
                      <template v-for="(day, i) in showingCal" :key="i" >
                        <td v-if="(i >20 &&i<28) && (!dataList[showingYear][showingMonthlyCount][day.date] || day.additional) " :class="[day.additional ? 'prev-month' : '' ]"
                        class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>

                        <td v-if="(i >20 &&i<28) && dataList[showingYear][showingMonthlyCount][day.date] && !day.additional" :class="[day.additional ? 'prev-month' : '' ]"
                        :style="{backgroundColor: moodStyle[dataList[showingYear][showingMonthlyCount][day.date].mood], color: textColor[dataList[showingYear][showingMonthlyCount][day.date].mood]}" class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>
                      </template>
                    </tr>

                    <tr>
                      <template v-for="(day, i) in showingCal" :key="i" >
                        <td v-if="(i >27 &&i<35) && (!dataList[showingYear][showingMonthlyCount][day.date] || day.additional) " :class="[day.additional ? 'prev-month' : '' ]"
                        class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>

                        <td v-if="(i >27 &&i<35) && dataList[showingYear][showingMonthlyCount][day.date] && !day.additional" :class="[day.additional ? 'prev-month' : '' ]"
                        :style="{backgroundColor: moodStyle[dataList[showingYear][showingMonthlyCount][day.date].mood], color: textColor[dataList[showingYear][showingMonthlyCount][day.date].mood]}" class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>
                      </template>
                    </tr>

                    <tr>
                      <template v-for="(day, i) in showingCal" :key="i" >
                        <td v-if="(i >34 &&i<42) && (!dataList[showingYear][showingMonthlyCount][day.date] || day.additional) " :class="[day.additional ? 'prev-month' : '' ]"
                        class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>

                        <td v-if="(i >34 &&i<42) && dataList[showingYear][showingMonthlyCount][day.date] && !day.additional" :class="[day.additional ? 'prev-month' : '' ]"
                        :style="{backgroundColor: moodStyle[dataList[showingYear][showingMonthlyCount][day.date].mood], color: textColor[dataList[showingYear][showingMonthlyCount][day.date].mood]}" class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>
                      </template>
                    </tr>

                    <tr>
                      <template v-for="(day, i) in showingCal" :key="i" >

                        <td v-if="(i > 41&&i<49) && (!dataList[showingYear][showingMonthlyCount][day.date] || day.additional) " :class="[day.additional ? 'prev-month' : '' ]"
                        class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>

                        <td v-if="(i > 41&&i<49) && dataList[showingYear][showingMonthlyCount][day.date] && !day.additional" :class="[day.additional ? 'prev-month' : '' ]"
                        :style="{backgroundColor: moodStyle[dataList[showingYear][showingMonthlyCount][day.date].mood], color: textColor[dataList[showingYear][showingMonthlyCount][day.date].mood]}" class="circle" @click="edit(showingYear,showingMonthlyCount,day.date,day.yoobi,day.additional)">{{day.date}}</td>
                      </template>
                    </tr>
          
                  </tbody>
          
                </table>
                <!-- <span>{{moodStyle[dataList[showingYear][showingMonthlyCount][3].mood]}}</span> -->
          
              </div>

              
              
               <!-- end calendar-container -->
        
            </div> <!-- end container -->
    
            <!-- <Calendar title-position="left" />
            <DatePicker title-position="left" v-model="date"  /> -->

            <!-- <div>
              <h1>Calendar</h1>
              
              <div class="month">      
                <ul>
                  <li class="prev">&#10094;</li>
                  <li class="next">&#10095;</li>
                  <li>
                    {{showingCal.month}}<br>
                    <span style="font-size:18px">{{showingCal.year}}</span>
                  </li>
                </ul>
              </div>

              <ul class="weekdays">
                <li>Mo</li>
                <li>Tu</li>
                <li>We</li>
                <li>Th</li>
                <li>Fr</li>
                <li>Sa</li>
                <li>Su</li>
              </ul>

              <ul class="days">  
                <li>1</li>
                <li>2</li>
                <li>3</li>
                <li>4</li>
                <li>5</li>
                <li>6</li>
                <li>7</li>
                <li>8</li>
                <li>9</li>
                <li><span class="active">10</span></li>
                <li>11</li>
                <li>12</li>
                <li>13</li>
                <li>14</li>
                <li>15</li>
                <li>16</li>
                <li>17</li>
                <li>18</li>
                <li>19</li>
                <li>20</li>
                <li>21</li>
                <li>22</li>
                <li>23</li>
                <li>24</li>
                <li>25</li>
                <li>26</li>
                <li>27</li>
                <li>28</li>
                <li>29</li>
                <li>30</li>
                <li>31</li>
                <li>1</li>
                <li>2</li>
                <li>3</li>
                <li>4</li>
              </ul>
            </div>  -->

            
            

            <!-- <div>
              <h5>{{showingCal}}</h5>
            </div> -->

          </div>
        </div>
      </div>
      
    </div>

  

  

   
  
</body>

  
  
 
</template>

<script>

export default {
  name: 'App',

  data() {
    return{
      showingPage: 'main',
      developing: true,
      showingDate: undefined,
      selectingNum: 6,
      actualContent: '',
      showingTextarea: false,
      moodNum: undefined,
      moodText: undefined,
      moodColor: undefined,
      userName: undefined,
      // localName: 'nisino25',
      userData: [],
      dataList: [],
      showingDataList: [],
      showingCal: {},
      showingMonth: undefined,
      showingYear: undefined,
      
      selectingDate: {},
      moodStyle: ['','DarkBlue','CornflowerBlue','Seagreen','Coral','#ff1919'],
      textColor: ['black','white','white','white','white','white'],

      preCord: undefined,
      aftCord: undefined,
      editing: {
        content: undefined,
        year: undefined,
        month: undefined,
        date: undefined,
        yoobi: undefined,
        mood: undefined,
      },

      selectingYear: undefined,

      



    };
  },
  mounted(){
    if(this.developing){
      // this.showingPage = 'input'
      this.showingPage = 'calendar'
      this.userName = 'Nozomu'
    }

    // localStorage = []
    if(localStorage.firstTime){
      console.log('found it')

      this.dataList = JSON.parse(localStorage.dataList);  
      this.showingDataList = this.createShowingCal()
    }else{
      console.log('welcome and now creating') 
      let flag = false
      localStorage.firstTime = JSON.stringify(flag); 
      
      this.createCalendar();
      localStorage.dataList = JSON.stringify(this.dataList); 
      localStorage.showingDataList = this.createShowingCal()
    }

    // this.addRandomData(2021,7)
    


    

     let dateObj = new Date();

    let year = dateObj.getFullYear()
    let month = dateObj.getMonth()+ 1

    this.showingCal =this.showingDataList[year][month]
    // console.log(this.showingDataList[year][month])
    this.showingYear = year
    this.selectingYear = year

    let monthlyList = ['','Jan','Feb','Mar','Apr','May','Jun','July','Aug','Sep','Oct','Nov','Dec',]
    this.showingMonth = monthlyList[month]
    this.showingMonthlyCount = month

    // this.dataList[2021][9][9].mood = 3
  },
  created(){
    // this.addRandomData()

    // let monthLength = undefined
    // let firstYoobi = undefined
    // this.showingDate = this.today
    // var dateObj = new Date();
    // console.log(dateObj.getFullYear())
    // console.log(dateObj.getMonth()+1)

    // this.userData.push({hye: 'hey', 2022: []})
    // this.userData = {2021: [],2022: []};
    // this.userData[2021] = {Jan: {},Feb: {},Mar: {},Apr: {},May: {},Jun: {},Jul: {},Aug: {},Sep: {},Oct: {},Nov: {},Dev: {}}
    // this.userData[2021] = [[],[],[],[],[],[],[],[],[],[],[],[],[]]
    // console.log(this.userData[2021])
    // var date = new Date();
    // var firstDay = new Date(date.getFullYear(), date.getMonth(), 1);
    // var lastDay = new Date(date.getFullYear(), date.getMonth() + 1, 0);

    // console.log(firstDay)
    // 

    // trying to get
    // var FirstDay = new Date(1999, 5, 1);
    // FirstDay = FirstDay.toString()
    // var LastDay = new Date(1999, 6, 0);
    // LastDay = LastDay.toString()
    
    
    // firstYoobi = FirstDay.split(' ')[0]
    // monthLength = Math.floor(LastDay.split(' ')[2])
    // console.log(firstYoobi)
    // console.log(monthLength)


    // --------------------------------
    // yoobiCount = firstYoobi
    // console.log(yoobiCount)
    // console.log('---------------------')
    // let firstYoobi = 'Mon'
    // console.log(this.getCalendar(2020,2))
    // this.getCalendar(2021,5)
    // this.makingFakeList()

    

  },
  computed:{
    today: function(){
      var dateObj = new Date();
      var month = dateObj.getMonth() + 1; //months from 1-12
      var day = dateObj.getDate();
      // var year = dateObj.getFullYear();
      let dayOfWeek = ['Sun','Mon','Tue','Wed','Thu','Fri','Sat',]
      let yoobi = dayOfWeek[dateObj.getDay()]

      return month + '/'+ day + ' ' + yoobi;
    },
    DateList: function (){
      let count = 0
      let theList = []
      let startingDate = -6
      while(count < 7){
        let yesterday = new Date(new Date().setDate(new Date().getDate() + startingDate));
        let dayOfWeek = ['Sun','Mon','Tue','Wed','Thu','Fri','Sat',]
        var month = yesterday.getMonth() + 1; //months from 1-12
        var day = yesterday.getDate();
        let yoobi = dayOfWeek[yesterday.getDay()]
        theList.push(month + '/'+ day + ' ' + yoobi)
        count++
        startingDate++
      }

      return theList
    },
    contentLength: function(){
      return this.actualContent.length
    },

  },
  methods:{

    setCalendar(){
      this.showingYear = this.selectingYear

      if(this.showingyear<1998 || this.showingYear > 2100 || this.showinMonth < 1||this.showingMonth > 12){
        alert('Type valid number please')
        return
      }
      this.showingCal = this.showingDataList[this.showingYear][this.showingMonthlyCount]

      let monthlyList = ['','Jan','Feb','Mar','Apr','May','Jun','July','Aug','Sep','Oct','Nov','Dec',]
      this.showingMonth = monthlyList[this.showingMonthlyCount]
    },

    createCalendar(){
      


      
      // first one year 
      let Mcount = 1; // Mcount max should be 12 then reset
      let Ycount = 1998; // Mcount max should be 100 then end the whole loop

      let dataList = {}
      let showingDataList = {}


      while(Ycount < 2100){
        dataList[Ycount] = {}
        showingDataList[Ycount] = {}
        Mcount = 1
        while(Mcount < 13){
          dataList[Ycount][Mcount] = this.getCalendar(Ycount,Mcount)
          // let fakeList =(dataList[Ycount][Mcount]).concat()

          showingDataList[Ycount][Mcount] = this.makingFakeList(dataList[Ycount][Mcount],Ycount,Mcount)

          Mcount++
        }
        Ycount++  
        
      }

      this.showingDataList = showingDataList
      this.dataList = dataList
      
      // console.log(dataList[2021][6])
      // console.log(showingDataList[2021][6])

      // change the calendar page as well 

    },

    createShowingCal(){
      let Mcount = 1; // Mcount max should be 12 then reset
      let Ycount = 1998; // Mcount max should be 100 then end the whole loop

      // let dataList = {}
      let showingDataList = {}


      while(Ycount < 2100){
        showingDataList[Ycount] = {}
        Mcount = 1
        while(Mcount < 13){
          // let fakeList =(dataList[Ycount][Mcount]).concat()

          showingDataList[Ycount][Mcount] = this.makingFakeList(this.dataList[Ycount][Mcount],Ycount,Mcount)

          Mcount++
        }
        Ycount++  
        
      }

      return showingDataList
    },

    sendData(){
      if(this.contentLength == 0){
        alert('Please type something')
        return
      }

      if (!window.confirm("Ready to send data?")) {
        return
      }
      
      

      let theString = this.DateList[this.selectingNum]
      console.log(theString)

      this.selectingDate.year = new Date().getFullYear()
      this.selectingDate.month = Math.floor(theString.split('/')[0])
      theString = theString.split('/')[1]
      this.selectingDate.day = Math.floor(theString.split(' ')[0])
      


      console.log((this.selectingDate))
      this.dataList[this.selectingDate.year][this.selectingDate.month][this.selectingDate.day].nikki.push(this.actualContent)
      console.log(this.dataList[this.selectingDate.year][this.selectingDate.month])
      this.dataList[this.selectingDate.year][this.selectingDate.month][this.selectingDate.day].mood = this.moodNum
      this.moodNum = undefined

      this.actualContent = ''

      // console.log(showingDataList[2021][6])



      //-----//-----//-----//-----//-----//----- //-----//-----
      // before add
      // check if the list is completed or not
      // then add the date data
      // nisino25[2021][4][2] that sis 2021/4/2



      // var FirstDay = new Date(year, month-1, 1);
      // FirstDay = FirstDay.toString()
      // var LastDay = new Date(year, month, 0);
      // LastDay = LastDay.toString();



      // gotta create the data untill it reach to the nearest future or month
      // data structure should be like year and month? 

      // when you add the data create the whole month and reach to the nearest future or month

    },

    addRandomData(year,month){
      let count = 1
      let randomNum = undefined
      let randomMood = undefined
      let theText = 'And once the storm is over, you won’t remember how you made it through, how you managed to survive. You won’t even be sure, whether the storm is really over. But one thing is certain. When you come out of the storm, you won’t be the same person who walked in. That’s what this storm’s all about.'

      while(count < this.dataList[year][month].length){
        randomNum = 1 + Math.floor(Math.random() * (10));
        if(randomNum>2){

          
          this.dataList[year][month][count].nikki.push(theText)

          randomMood = 1 + Math.floor(Math.random() * (5));
          this.dataList[year][month][count].mood = randomMood

          // console.log(`Hi: ${count}}`)
        }
        count++ 
      }

      // skip the index 0 and add the data with 30% of chances

    },

    // ---------------------------------------------------


    getCalendar(year, month){
      if(month > 12){
        alert('month has to be 12 or under')
        return 
      }
      // get yoobi and the month length
      var FirstDay = new Date(year, month-1, 1);
      FirstDay = FirstDay.toString()
      var LastDay = new Date(year, month, 0);
      LastDay = LastDay.toString();

      // this.showingCal.year = year
      // let monthlyList = ['','Jan','Feb','Mar','Apr','May','Jun','July','Aug','Sep','Oct','Nov','Dec',]
      // this.showingCal.month = monthlyList[month]
      // this.showingCal.monthCount = month


      
      
      let firstYoobi = FirstDay.split(' ')[0]
      let monthLength = Math.floor(LastDay.split(' ')[2])
      let yoobiCount = undefined  
      switch(firstYoobi){
        case 'Sun':
          yoobiCount = 0
          break;

        case 'Mon':
          yoobiCount = 1
          break;

        case 'Tue':
          yoobiCount = 2
          break;

        case 'Wed':
          yoobiCount = 3
          break;
        
        case 'Thu':
          yoobiCount = 4
          break;

        case 'Fri':
          yoobiCount = 5
          break;

        case 'Sat':
          yoobiCount = 6
          break;
      }

      
      
      // console.log(monthLength)
      let yoobiList =['Sun','Mon','Tue','Wed','Thu','Fri','Sat','Sun','Mon','Tue','Wed','Thu','Fri','Sat','Sun','Mon','Tue','Wed','Thu','Fri','Sat','Sun','Mon','Tue','Wed','Thu','Fri','Sat','Sun','Mon','Tue','Wed','Thu','Fri','Sat','Sun','Mon','Tue','Wed','Thu','Fri','Sat',]

      let list = []
      let count = 1


      // in order to remove index 0
      let previousLastDay =new Date(year, month-1, 0).toString();
      // let previousLastYoobi = previousLastDay.split(' ')[0]
      previousLastDay = Math.floor(previousLastDay.split(' ')[2])
      list.push({date: previousLastDay, yoobi: yoobiList[yoobiCount+6],additional: true,  nikki:[], mood: 0, })
 



      while(count <= monthLength){
        list.push({date: count, yoobi: yoobiList[yoobiCount],additional: false, nikki:[],mood: 0,})
        count++
        yoobiCount++
      }
      
      // console.log(yoobiCount)
      
      // this.showingCal.cal = list
      // this.makingFakeList()

      return list;
    },

    getYoobiCount(yoobi){
      let yoobiCount = undefined
      switch(yoobi){
        case 'Sun':
          yoobiCount = 0
          break;

        case 'Mon':
          yoobiCount = 1
          break;

        case 'Tue':
          yoobiCount = 2
          break;

        case 'Wed':
          yoobiCount = 3
          break;
        
        case 'Thu':
          yoobiCount = 4
          break;

        case 'Fri':
          yoobiCount = 5
          break;

        case 'Sat':
          yoobiCount = 6
          break;
      }
      return yoobiCount
    },

    getMonthCount(tsuki){
      let tsukiCount = undefined
      // console.log('you called?')
      switch(tsuki){
        case 'Jan':
          tsukiCount = 1
          break;

        case 'Feb':
          tsukiCount = 2
          break;

        case 'Mar':
          tsukiCount = 3
          break;
        
        case 'Apr':
          tsukiCount = 4
          break;

        case 'May':
          tsukiCount = 5
          break;

        case 'Jun':
          tsukiCount = 6
          break;
        
        case 'Jul':
          tsukiCount = 7
          break;
        
        case 'Aug':
          tsukiCount = 8
          break;
        
        case 'Sep':
          tsukiCount = 9
          break;
        
        case 'Oct':
          tsukiCount = 10
          break;
        
        case 'Nov':
          tsukiCount = 11
          break;
        
        case 'Dec':
          tsukiCount = 12
          break;

        
      }
      return tsukiCount
    },
    
    makingFakeList(fakeList,year,month){
      let yoobiList =['Sun','Mon','Tue','Wed','Thu','Fri','Sat','Sun','Mon','Tue','Wed','Thu','Fri','Sat','Sun','Mon','Tue','Wed','Thu','Fri','Sat','Sun','Mon','Tue','Wed','Thu','Fri','Sat','Sun','Mon','Tue','Wed','Thu','Fri','Sat','Sun','Mon','Tue','Wed','Thu','Fri','Sat',]
      // const sheeps = ['🐑', '🐑', '🐑'];

      // const fakeSheep = sheeps;
      // const cloneSheeps = [...sheeps];

      
      

      let yoobiCount = undefined

      // dataList[Ycount][Mcount]=  dataList[Ycount][Mcount].slice(1)
      // if(year == 2021 && month == 12){
      //   console.log(fakeList)
      // }
      

      fakeList = fakeList.slice(1)
      if(year == 2021 && month == 3){
        // console.log(fakeList)
      }

      // impoooooooooooooooooooooooooooooooooooooooooooooooogant
      

      // make the first line of the week /

      // in order to remove index 0
      let previousLastDay =new Date(year, month-1, 0).toString();
      let previousLastYoobi = this.getYoobiCount( previousLastDay.split(' ')[0])
      previousLastDay = Math.floor(previousLastDay.split(' ')[2])
      // list.push({date: previousLastDay, yoobi: previ, nikki:[], })



      yoobiCount = this.getYoobiCount(fakeList[0].yoobi)
      // console.log(yoobiCount)

      let whileCount = 0

      // yoobicount is 4 this case
      // in this case do thur, wed, tue, mond
      previousLastDay++
      previousLastYoobi++

      if(yoobiCount == 0){
        yoobiCount = 7
      }

    
      while(whileCount <  yoobiCount -1){
        previousLastDay--
        previousLastYoobi--
        fakeList.unshift({date: previousLastDay, yoobi: yoobiList[previousLastYoobi], additional: true, nikki:[],});
        whileCount ++ 
      }

      // ---------------------------------------------------------------------------
      // get day of course 1st
      // get day of course yoobi for the shit

      // if the last day was 7 then it should be fine
      // if the last day was 6 then do it once
      // if the last day was 1 then do it 6 times

      whileCount = 0
      let lastDay = 0
      let lastYoobi = this.getYoobiCount(fakeList[fakeList.length -1].yoobi)
      if(lastYoobi == 0){
        lastYoobi+=7
      }
      // let theYoobi = lastYoobi

    
      while(lastYoobi < 7){
        lastDay++
        lastYoobi++
        fakeList.push({date: lastDay, yoobi: yoobiList[lastYoobi], additional: true, nikki:[],});
        whileCount ++ 
      }

      // Talking about the previous day. If it is 7 then it should stop, if 1 then do it only once, if 6 then do it 6 times


      

      


      // so basically fill up the empty space of the first and last weeek
      // this.showingCal.cal = fakeList

      // console.log(this.showingCal.cal)
      return fakeList
    },
    // ---------------------------------------------------------------

    edit(year,month,date,yoobi,flag){

      if(flag){
        return
      }

      this.editing.content = this.dataList[year][month][date].nikki
      this.editing.year = year
      this.editing.month = month
      this.editing.date = date
      this.editing.yoobi = yoobi
      this.editing.mood = this.dataList[year][month][date].mood

      this.showingPage = 'editing'
      console.log(this.dataList[year][month][date].mood)

      if(this.dataList[year][month][date].mood !== 0){
        this.showingTextarea = true
        this.moodNum = this.editing.mood
      }

      // console.log(year,month,date)

    },

    updateData(){
      if(this.editing.content == 0){
        alert('Please type something')
        return
      }

      if (!window.confirm("Ready to update data?")) {
        return
      }
      // nikki and 
      this.dataList[this.editing.year][this.editing.month][this.editing.date].nikki = this.editing.content

      this.dataList[this.editing.year][this.editing.month][this.editing.date].mood =  this.editing.mood

      this.showingPage = 'calendar'
      this.showingYear = this.editing.year
      this.showingMonthlyCount = this.editing.month
      this.setCalendar()

    },


    // ---------------------------------------------------------------
    tStart(e){
      this.preCord =e.touches[0].clientX
      console.log(this.preCord)
    },
    tEnd(e){
      this.aftCord = e.changedTouches[0].clientX
      console.log(this.aftCord)
    },
  },
  watch:{
    selectingNum: function(){
      this.showingDate = this.DateList[this.selectingNum]
      console.log('called')
      
    },

    moodNum: function(){
      if(this.moodNum){
        this.showingTextarea = true
      }else{
        this.showingTextarea = false
      }

      switch(this.moodNum){
        
        
        case 1:
          this.moodText = 'sentiment_very_dissatisfied'
          this.moodColor = 'DarkBlue'
          break;

        case 2:
          this.moodText = 'sentiment_dissatisfied'
          this.moodColor = 'CornflowerBlue'
          break;

        case 3:
          this.moodText = 'sentiment_neutral'
          this.moodColor = 'Seagreen '
          break;

        case 4:
          this.moodText = 'sentiment_satisfied'
          this.moodColor = 'Coral'
          break;

        case 5:
          this.moodText = 'sentiment_very_satisfied'
          this.moodColor = '#ff1919'
          break;
        


        
      }
    },

    dataList: {
      deep:true,
      handler() {
        localStorage.dataList = JSON.stringify(this.dataList); 
      }
    },

    aftCord: function(){
      if(this.aftCord - this.preCord>= 60 ){
        console.log('swiped: left')
        if(this.showingYear == 1998 && this.showingMonthlyCount == 1){
          return 
        }

        if(this.showingMonthlyCount !== 1){
          this.showingMonthlyCount--
          this.setCalendar()
        }else{
          this.showingYear--
          this.selectingYear--
          this.showingMonthlyCount = 12
          this.setCalendar()
        }
      }

      if(this.preCord - this.aftCord >= 60){
        console.log('swiped: right')
        if(this.showingYear == 2099 && this.showingMonthlyCount == 12){
          return 
        }

        if(this.showingMonthlyCount !== 12){
          this.showingMonthlyCount++
          this.setCalendar()
        }else{
          this.showingYear++
          this.selectingYear++
          this.showingMonthlyCount = 1
          this.setCalendar()
        }
      }
    },
  }
  
}
</script>

<style>

/* body {
  background-color: #fbab7e;
  background-image: linear-gradient(62deg, #fbab7e 0%, #f7ce68 100%);
 
  font: 87.5%/1.5em "Lato", sans-serif;
  margin: 0;
} */

table {
  border-collapse: collapse;
  border-spacing: 0;
}
 
td {
  padding: 0;
  /* color: red  */
}
 
/* .container {
  height: 600px;
  left: 50%;
  margin: -300px 0 0 -300px;
  position: absolute;
  top: 50%;
  width: 80%
} */
 
.calendar-container {
   /* position: relative;   */
  margin-top: 20px;
  width: 450px; 
  width: 100%;  
  display: block;
  margin-left: auto;
  margin-right: auto;
  /* left:50%; */
  /* background-color: yellow; */
}
 
.calendar-container header {
  border-radius: 1em 1em 0 0;
  background: #e66b6b;
  color: #fff;
  padding: 2em 2em;
  /* height: 20%; */
  /* width: 80%; */
}
 
.month {
  /* width: 50%; */
  font-size: 4em;
  font-weight: 900; 
  line-height: 1em;
  text-align: left;
  margin-left: -10px;
}
 
.year {
  font-size: 2em;
  line-height: 1em;
  text-transform: lowercase;
  text-align: left;
  /* margin-left: 10px; */
}

/* ------------------------------------------------------------------ */
 
.calendar {
  background: #fff;
  border-radius: 0 0 1em 1em;
  -webkit-box-shadow: 0 2px 1px rgba(0, 0, 0, 0.2), 0 3px 1px #fff;
  box-shadow: 0 2px 1px rgba(0, 0, 0, 0.2), 0 3px 1px #fff;
  color: #555;
  display: inline-block;
  /* padding: 2em; */
  width: 100%;
  /* padding-bottom: 100px; */
  padding-top: 20px;
  padding-bottom: 20px;
  padding-left: 20px;
}
 
.calendar thead {
  color: #e66b6b;
  font-weight: 700;
  text-transform: uppercase;
  /* margin-top: 100px; */
  padding-top: 100px;
}
 
.calendar td {
  padding: 0.5em 1em; 
  padding: 5px 5px; 
  margin-right: 100px; 
  text-align: center;
  /* width:100%; */
 
}
.circle{
    /* border-radius: 50%;
    width: auto;
    height: auto; 
    background-color: yellow; */

}
 
.current-day {
  color: #e66b6b;
}
 
.prev-month,
.next-month {
  color: #b8aeae;
}

 

/* ----------------------------------------------------------- */

.mood-btn{
  display:inline-block;
  margin-right: 5px;
  margin-left: 5px;
  /* font-size: 200%; */
}


select{
  border-radius: 25px;
}

.seleting-mood{
font-size:480px;  
}

.textarea{
  transition: opacity 3.5s;
}



.slide-fade-enter-active {
  transition: all 0.8s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}

/* -------------------------------------- */

.topBar{
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 85%;
}

.button {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 8px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 12px;
  margin: 4px 2px;
  cursor: pointer;
}

.button1 {border-radius: 8px;}

/* -------------------------------------- */
#app {
  width: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

.menu-bar{
  /* background-color: rgb(26, 115, 232);; */
  /* background-color: DarkSlateBlue; */
  background-color: SteelBlue;
  position:fixed;
  padding:0;
  margin:0;

  top:0;
  left:0;
  padding-top: 10px;
  /* padding-left: 10px; */

  width: 100%;
  height: 75px;
  color:white;
}

.menu-left-btn{
  float: left;
  margin-left: 12px;
} 

.menu-right-btn{
  float: right;
  margin-right: 12px;
  font-size: 150%;
}

/* ------------------------------------------------- */
.card {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 85%;
  padding: 15px 10px;
  margin: auto;
  background-color: SlateBlue;
  /* width: 50%; */
  /* border: 3px solid green; */
  /* padding: 10px; */
  border-radius: 25px;
  color:SeaShell
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.card li{
  list-style-type: none;
  white-space: nowrap;
  overflow: hidden; 
  text-overflow: ellipsis;
  white-space: nowrap;

}

.container .arrow{
  font-size:100%;
  margin-top:4px
}

.container .callendar{
  font-size:200%;
  /* text-align:right; */
  float: right;
  margin-right: 10px;
  /* flot:right */
 
}

.card-bottom .demo{
  padding: 20px;
  margin-top: -15px;
  /* background-color: yellow; */
}

.selecteDate{
  background: #dbd7d2;
  /* background: red; */
  width: 80px;
  /* height: 40px; */
  border-radius: 50%;
  text-align: center;
  /* line-height: 50px; */
  padding: 12.5px;
  vertical-align: middle;
  color: black
}


/* ------------------------------------------------------------------ */
.main-part{
  /* text-align: center; */
	/* top: 50%; */
	/* transform: 	translateY(-50%); */
}
.main-part span{
  font-size: 140%;
  margin-left: 20px;
  float:left;
  text-align: left;
  

}


/* ---------------------------- */
.main-part ul{
  list-style-type: none;
}

.task-card {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 85%;
  padding: 15px 10px;
  margin: auto;
  background-color: grey;
  /* width: 50%; */
  /* border: 3px solid green; */
  /* padding: 10px; */
  border-radius: 10px;
  color:SeaShell;
  text-align: center;
}

body{
  overflow: hidden;
}
  

.visible {
  visibility: visible;
  opacity: 1;
  transition: opacity 2s linear;
}

.slide-fade-enter-active {
  transition: all 0.5s ease-out;
}
.slide-fade-leave-active {
  transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
   opacity: 0;
}

</style>
