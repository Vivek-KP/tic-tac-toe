<script>
export default {
  data() {
    return {
      init:'X',
      result:[['','',''],['','',''],['','','']],
      alternate:true
    }
  },
  methods:{
    insert(i,j){
      console.log(i,j)
      if(this.result[i][j] === ''){
        if(this.alternate){
          this.result[i][j] = 'X';
          this.init = 'X'
        }else{
          this.result[i][j] = 'O';
          this.init = 'O'

        }
        console.log(this.result)
        this.alternate = !this.alternate
      }
    },
    reset(){
      this.result= [['','',''],['','',''],['','','']]
      this.alternate = true
      this.init = 'X'
    }
  },
  computed:{
    checkWin(){
      for(let i =0;i<this.result.length;i++){
        if(this.result[i].every(row=>row===this.init )){
          return true
        }
      }
      for(let j =0;j<this.result.length;j++){
          if(this.result.every(col=>(col[j]===this.init))){
            return true
          }
      }
      if(this.result.every((row,index)=>row[index]===this.init)){
        return true
      }
      if(this.result.every((row,index)=>row[(this.result.length)-1-index]===this.init)){
        return true
      }
        return false
    },
    checkDraw(){
      let col = true
      let row = true
      for(let i =0;i<this.result.length;i++){
        if(this.result[i].some(row=>row==='' )){
          row =  false
        }
      }
      for(let j =0;j<this.result.length;j++){
          if(this.result.some(col=>(col[j]===''))){
            col =  false
          }
      }
      if(col && row ){
        return true
      }else
        return false
    }
  }
}
</script>

<template>
  <div>
 <div class="horizontal" v-for="(row,rowIndex) in result">
    <div  v-for="(col,colIndex) in row">
      <div>
      <button class="btn" :disabled="checkWin" @click="insert(rowIndex,colIndex)">{{col}}
        </button>
        
      </div>
    </div>

 </div>
 <div v-if="checkWin || checkDraw" >
 <button @click="reset()" class="resetButton">Restart</button>
<p v-if="checkWin" > <b>{{ init }}</b> has won the match</p>
<p v-else>It's a Tie</p>
 </div>
  </div>
</template>

<style>
.btn{
  height: 70px;
  width: 70px;
  margin: 1px;

}
.horizontal{
  display: flex;
}

p{
  color: green;
}

.resetButton{
  background-color: rgb(106, 90, 205);
  color: white;
  border: none;
  padding: 5px 18px;
  border-radius: 8px;
  margin-top: 8px;
}
</style>