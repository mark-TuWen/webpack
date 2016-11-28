<template>
  <div id="app" v-bind:style="{margin:'20px auto'}">
     <p>{{ msg }}</p>
     <input type="text" v-model="msg"/>
     <ul class="pagination">
       <li v-for="n in pageCount">
          <a v-bind:class="activeNumber === n ? 'active' : ''">{{ n }}</a>
       </li>
     </ul>

     <fieldset>
        <div :class="'file-group'">
           <label>Name:</label>
           <input type="text" v-model="newPeople.name" placeholder="请输入姓名" />
        </div>
        <div :class="'file-group'">
           <label>Age:</label>
           <input type="text" v-model="newPeople.age" placeholder="请输入姓名" />
        </div>
        <div :class="'file-group'">
           <label>sex:</label>
           <select v-model="newPeople.sex">
              <option value="male">male</option>
              <option value="female">female</option>
           </select>
        </div>
        <div :class="'file-group'">
           <button v-bind:class="'deletes'" @click="greatePerson($index)">Greate</button>
        </div>
     </fieldset>
     <input type="checkbox" id="checkbox" v-model="checked">
     <label for="checkbox">{{ checked }}</label>
     <input type="number" v-model.number="age">
     <!-- <table class="static" v-bind:class="{'actived':isActive, 'text-danger':hasError}"> -->
     <table class="static" v-bind:class="classObj">
       <thead>
         <tr>
           <!-- click事件直接绑定一个方法 -->
           <th v-on:click="great">name</th>
           <!-- 事件使用内联语句 -->
           <th v-on:click="say">age</th>
           <!-- v-bind:class 缩写 :class  v-on:click 缩写 @click -->
           <th :class="'active'" @click="great">sex</th>
           <th>delete</th>
         </tr>
       </thead>
       <tbody>
         <tr v-for="item in people">
           <td v-bind:style="{color:activeColor, fontSize: fontSize +'px'}">{{item.name}}</td>
           <td v-bind:style="styleObj">{{item.age}}</td>
           <td>{{item.sex}}</td>
           <td><button :class="'deletes'" @click="deletePerson()">delete</button></td>
         </tr>
       </tbody>
     </table>
    
      <span v-for="n in even(numbers)">{{n}}</span>
      <button v-on:keyup.enter="counter += 1">增加1</button>
      <p>这个按钮被点击了 {{ counter }} 次。</p>
      <button v-on:click="show = !show">
        Toggle
      </button>
      <transition name="slide-fade">
      <!-- <transition name="fade"> -->
        <p v-if="show">hello</p>
      </transition>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      msg : 'vue',
      show:true,
      counter:0,
      activeNumber: 1,
      pageCount: 10,
      isActive: true,
      hasError: true,
      activeColor: 'red',
      fontSize: 24,
      numbers:[1,2,3,4,5,6,7],
      styleObj:{
        color:'blue',
        fontSize:'18px',
        transform:'translateY(10px)'
      },
      classObj:{
        'active':true,
        'textdanger':false
      },
      newPeople:{
        name: '',
        age: 0,
        sex: 'male'
      },
      people : [
          {
            name: 'jack',
            age: 30,
            sex: 'male'
          },
          {
            name: 'bill',
            age: 26,
            sex: 'male'
          },
          {
            name: 'tracy',
            age: 22,
            sex: 'female'
          },
          {
            name: 'next',
            age: 42,
            sex: 'le'
          }
      ]
    }
  },
  methods:{
    great:function(){
       var ele = document.querySelector('input').value;
       alert(ele);
    },
    say:function(e){
       var target = e.target;
       target.style.color = 'red';
    },
    greatePerson:function(){
       this.people.push(this.newPeople);
       this.newPeople = {name:'',age:0,sex:'male'};
    },
    deletePerson:function(index){
       this.people.splice(index,1);
    },
    even:function(numbers){
       return numbers.filter(function(number){
          return number % 2 === 0;
       })
    }
  }
}

</script>

<style>
*{
  margin: 0;
  padding: 0;
}
.file-group{
  height: 30px;
}
.file-group input, .file-group select{
  height: 20px; margin-top: 5px; width: 240px;
}
.file-group button{
  padding: 5px 20px;
  margin: 5px 0px 5px 100px;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-active {
  opacity: 0
}

.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-active {
  padding-left: 10px;
  opacity: 0;
}
label{
  display: block;
  width: 120px;
  height: 30px;
  line-height: 30px;
  text-align: right;
  float: left;
  margin-right: 20px;
}
fieldset{
  padding: 10px 0; 
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background: #eee;
}
table{ 
  border: 1px solid #666;
}
td{
  width: 180px;
  height: 40px;
  border-left: 1px solid #666;
  border-top: 1px solid #666;
  text-align: center;
}
th{
  height: 30px;
  text-align: center;
  background: #42B983;
  color: #fff;
}
.pagination{height: 40px; width: 100%; margin: 10px;}
li{list-style-type: none; height: 40px; width: 40px; border: 1px solid #ccc; border-left: none; color: #666; float: left;}
a{display: block; cursor: pointer; width: 100%; height: 100%; text-align: center;line-height: 40px;}
.active{background: #31c872; color: #eee;}
.deletes{background: #42B983; color: #fff; padding: 5px; border: none; outline: none; border-radius: 3px;}
</style>
