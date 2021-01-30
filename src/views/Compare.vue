<template>
  <div class="compare">
    <div class="explain">
      트레할때 동료리스트 비교해가면서 하나한 겹치는 동료 찾기 귀찮아서 만든
      사이트<br />
      <br />
      이용방법<br />
      왼쪽 입력칸은 자신의 동료리스트를 복붙해놓는 칸<br />
      오른쪽 입력칸은 딴놈의 동료리스트를 복붙해놓는 칸<br />
      <br />
      구분분자는 만약 내가 "겜닉/그룹명" 이렇게 동료리스트를 작성했다고 했을따
      "/" 이게 구분문자<br />
      왼쪽칸은 자신의 구분문자 복붙하는 칸<br />
      오른칸은 딴놈의 구분문자 복붙하는 칸<br />
      <br />
      구분문자 쓸때 만약 "겜닉 / 그룹명" 이라고 썼으면 무조건
      "(띄어쓰기)/(띄어쓰기)" 일케쓰셈 <br />
      //보기 편하게 (띄어쓰기)라고 썼는데 진짜 (띄어쓰기)라고 쓸 놈 있을까봐 더
      쓰는건데 " " ← 이걸 쓰란 뜻임 " / " 일케<br />
      <br />
      만약 님은 "겜닉/그룹명" 으로 동료리스트 작성했는데<br />
      비교할 딴놈 껀 "겜닉/팀명" 으로 했으면 작동안함<br />
      무조건 그룹명이나 팀명이나 일치해야함<br />
    </div>
    <div class="dongryo-list">
      <v-textarea
        solo
        label="자신의 동료리스트"
        v-model="inputList1"
        style="margin: 5rem;"
      ></v-textarea>
      <v-textarea
        solo
        label="상대의 동료리스트"
        v-model="inputList2"
        style="margin: 5rem;"
      ></v-textarea>
    </div>
    <div class="divide-letter">
      <v-col cols="12" sm="6" md="3">
        <v-text-field
          label="본인 구분문자"
          v-model="after_letter"
          filled
        ></v-text-field>
      </v-col>
      <v-col cols="12" sm="6" md="3">
        <v-text-field
          label="상대 구분문자"
          v-model="before_letter"
          filled
        ></v-text-field>
      </v-col>
    </div>
    <div class="button">
      <v-btn elevation="2" @click="stringToArray">
        중개되는 놈 찾기
      </v-btn>
      <div class="list" :key="i" v-for="(data, i) in intermediary">
        {{ data }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "compare",
  data() {
    return {
      inputList1: "",
      inputList2: "",
      after_letter: "",
      before_letter: "",
      list1: [],
      list2: [],
      intermediary: "",
    };
  },
  methods: {
    stringToArray() {
      let a = this.after_letter;
      let b = new RegExp(this.before_letter, "gi");
      let replaced_str = this.inputList2.replace(b, a);
      this.list1 = this.inputList1.split("\n");
      this.list2 = replaced_str.split("\n");
      this.compareList();
    },
    compareList() {
      var compareList = new Set(this.list2);
      this.intermediary = [
        ...new Set(this.list1.filter((x) => compareList.has(x))),
      ];
      if (this.intermediary.length == 0) this.intermediary = "X";
    },
  },
};
</script>

<style>
.dongryo-list {
  display: flex;
  justify-content: center;
}

.divide-letter {
  width: 100%;
  display: flex;
  justify-content: space-around;
}

.button {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.list {
  margin: 1rem;
  font-size: 30px;
}

.explain {
  border: 1px solid black;
  margin: 1rem;
  padding: 1rem;
  text-align: center;
}
</style>
