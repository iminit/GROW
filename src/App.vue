<template>
    <div id="app">
        <div class="question">
            <h1>{{questions[index].q}}</h1>
            <template v-if="questions[index].t">
                <mt-field label="" placeholder="输入你的答案" v-model="answer" @keyup.enter="nextQuestion"></mt-field>
            </template>
            <!--<mt-progress :value="progress">-->
                <!--<div slot="start">0</div>-->
                <!--<div slot="end">{{this.questions.length - 1}}</div>-->
            <!--</mt-progress>-->
            <mt-button @click.native="nextQuestion">下一题</mt-button>
        </div>
        <div class="answer" v-if="showAnswer">
            <template v-for="q,index in questions">
                <template v-if="q.t"><span>{{q.q}} 答：<b>{{q.a}}</b></span></template>
                <template v-else><h1>{{q.q}}</h1></template>
                <br>
            </template>
        </div>
    </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: "高绩效教练GROW辅导，请按照下面提示回答",
      questions: [
        {q:"Goal目标设定常用的问题",a:"",t:false},
        {q:"一，你的目标是什么？",a:"",t:true},
        {q:"二，如果你知道答案的话，那会是什么？",a:"",t:true},
        {q:"三，你具体的目标是什么？",a:"",t:true},
        {q:"四，你想什么时候实现？",a:"",t:true},
        {q:"五，实现目标的标志是什么？",a:"",t:true},
        {q:"六，如果需要量化的话，拿什么来量化你的目标？",a:"",t:true},
        {q:"Reality，关于现状常用的问题",a:"",t:false},
        {q:"一，目前的现状怎么样？",a:"",t:true},
        {q:"二，你如何知道这是准确的信息？",a:"",t:true},
        {q:"三，这是什么时候发生的？",a:"",t:true},
        {q:"四，这种情况发生的频率如何？",a:"",t:true},
        {q:"五，你都做你都做了些什么去实现目标？",a:"",t:true},
        {q:"六，都有谁与之相关？他们是什么态度？",a:"",t:true},
        {q:"七，是什么原因阻止你不能去实现目标？",a:"",t:true},
        {q:"八，和你有关的原因有哪些？",a:"",t:true},
        {q:"九，在目标不能实现的时候，你有什么感觉？",a:"",t:true},
        {q:"十，是什么令你……？",a:"",t:true},
        {q:"十一，其他的因素还有哪些？",a:"",t:true},
        {q:"十二，你都采用过哪些行动？",a:"",t:true},
        {q:"Options，你有哪些选择？",a:"",t:false},
        {q:"一，为改变目前的情况，你做过了什么？",a:"",t:true},
        {q:"二，可提供的选择有哪些？",a:"",t:true},
        {q:"三，你曾见过或听说过别人有哪些做法？",a:"",t:true},
        {q:"四，如果……会发生什么？",a:"",t:true},
        {q:"五，哪一种选择你认为最有可能成功？",a:"",t:true},
        {q:"六，这些选择有的优缺点是什么？",a:"",t:true},
        {q:"七，请陈述你觉得采取行动的可能性，并打分",a:"",t:true},
        {q:"八，调整哪一个指标，可能提高行动的可能性",a:"",t:true},
        {q:"Will，你要做什么？",a:"",t:false},
        {q:"一，下一步是什么？",a:"",t:true},
        {q:"二，何时是你采取下一步的最好时机？",a:"",t:true},
        {q:"三，可能遇到的障碍是什么？",a:"",t:true},
        {q:"四，你需要什么支持？",a:"",t:true},
        {q:"五，谁可能对此有帮助，",a:"",t:true},
        {q:"六，你何时需要支持，以及如何获得支持？",a:"",t:true},
        {q:"高绩效教练GROW辅导完毕",a:"",t:false}],
      index: 0,
      progress: 0,
      answer: "",
      showAnswer: true
    };
},
  mounted(){
    this.$toast(this.msg);
  },
  methods: {
    nextQuestion(){
      // 判断是否需要录入问题
      if(this.index == this.questions.length - 1){
        this.$toast("恭喜您回答完毕");
        this.showAnswer = true;
        return;
      }
      if(this.questions[this.index].t){
        if(!this.answer){
          this.$toast("请输入您的答案");
          return;
        }
        this.progress ++;
        this.questions[this.index].a = this.answer; // 把用户输入的答案存下来，这是上一问的答案
        this.answer = "";
      }
      // 把题目转到下一题
      this.index ++
    }
   }
}




</script>

<style>
.question {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.answer {
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}




</style>
