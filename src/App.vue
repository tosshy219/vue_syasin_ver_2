<template>
  <div id="app">
    <input type="radio" value="1" v-model="scale" name="scale-set" @click="reset()" />
    <span>1</span>
    <input type="radio" value="2" v-model="scale" name="scale-set" @click="reset()" />
    <span>2</span>
    <input type="radio" value="3" v-model="scale" name="scale-set" @click="reset()" />
    <span>3</span>
    <input type="radio" value="4" v-model="scale" name="scale-set" @click="reset()" />
    <span>4</span>
    <input type="radio" value="5" v-model="scale" name="scale-set" @click="reset()" />
    <span>5</span>
    <div class="btnWrapper">
      <p class="btn" @click="check(),deleter()">hide</p>
      <p class="btn" @click="start()">see</p>
      <p class="btn" @click="toNext() ,reset()">next</p>
    </div>
    <h1 class="info">{{scale}} x {{scale}}</h1>
    <div class="wrapper">
      <div
        v-for="n in pika"
        :key="n.id"
        class="content"
        :class="{check:confirm,see:n.check}"
        @click="see(n)"
      >
        <div class="left">
          <h1 class="leftLetter">{{shuffledLeft[n.num]}}</h1>
        </div>
        <div class="rightWrapper">
          <div class="right">
            <p class="name">{{shuffledName[n.num]}}</p>
            <p class="like">{{shuffledLike[n.num]}}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      names: [
        "A",
        "B",
        "C",
        "D",
        "E",
        "F",
        "G",
        "H",
        "K",
        "L",
        "M",
        "N",
        "O",
        "P",
        "R",
        "S",
        "T",
        "U",
        "V",
        "W",
        "X",
        "Y",
        "Z",
        "a",
        "b",
        "d",
        "e",
        "f",
        "g",
        "h",
        "i",
        "j",
        "k",
        "m",
        "n",
        "p",
        "q",
        "r",
        "t",
        "y"
      ],
      likes: [
        "アイスの実",
        "鮭",
        "塩辛",
        "ネギ",
        "マジカル",
        "めかじき",
        "ダンサー",
        "夜空",
        "ココア",
        "星",
        "ごま",
        "ギャング",
        "やくしゃ",
        "グラサン",
        "居眠り",
        "レース",
        "ケバブ",
        "ぞうさん",
        "銅像",
        "ネンド",
        "どんぐり",
        "よわむし",
        "ホイップ",
        "竹馬",
        "京都",
        "木星",
        "針",
        "ペルー",
        "カナダ",
        "メキシコ",
        "バンコク",
        "かめ",
        "にぼし",
        "マグロ",
        "すし",
        "鼻血",
        "クレープ",
        "アスリート",
        "ムール貝",
        "ナッツ",
        "モヒート",
        "スピネル",
        "エメラルド",
        "灰皿",
        "グアム",
        "ギャバ",
        "歌舞伎町",
        "キャバクラ",
        "メリケン",
        "ジャンケン",
        "しむらけん",
        "アキレス腱",
        "ピタゴラス",
        "しいたけ",
        "うろこ",
        "あんぱん",
        "レター",
        "バター",
        "砂鉄",
        "金",
        "銀",
        "ゴールド",
        "ルフィ",
        "ディズニー",
        "岩",
        "シルク",
        "かぜ",
        "雨",
        "パズル",
        "カフェイン",
        "口紅",
        "笑顔",
        "ぼうし",
        "なわとび",
        "安全靴",
        "りんだまん",
        "金髪",
        "アルビノ",
        "テラス",
        "台風",
        "地震",
        "火事",
        "雪",
        "草",
        "恐竜",
        "グミ",
        "チョコ",
        "せんべい",
        "かき氷",
        "宿題",
        "赤点",
        "ウォーター",
        "テニス",
        "ボクシング",
        "カラオケ",
        "がいこつ",
        "ゆうしゃ",
        "ムエタイ",
        "空手",
        "ラザニア",
        "はかせ",
        "コック",
        "ワクチン",
        "チワワ",
        "ジョーズ",
        "宝石",
        "カンフー",
        "竹林",
        "背骨",
        "とんこつ",
        "わたぱち",
        "銀河",
        "カレー",
        "判定",
        "レフリー",
        "リュック",
        "ミント",
        "スパイス",
        "じゃがいも",
        "レタス",
        "ベーコン",
        "ささみ",
        "ゲーマー",
        "弾薬",
        "青森",
        "岩手",
        "秋田",
        "北海道",
        "山形",
        "宮城",
        "福島",
        "新潟",
        "栃木",
        "茨城",
        "千葉",
        "東京",
        "埼玉",
        "群馬",
        "長野",
        "富山",
        "石川",
        "福井",
        "岐阜",
        "愛知",
        "山梨",
        "静岡",
        "滋賀",
        "三重",
        "奈良",
        "兵庫",
        "大阪",
        "和歌山",
        "鳥取",
        "岡山",
        "香川",
        "徳島",
        "高知",
        "愛媛",
        "広島",
        "島根",
        "山口",
        "福岡",
        "佐賀",
        "長崎",
        "熊本",
        "宮崎",
        "鹿児島",
        "沖縄"
      ],
      lefts: [
        "あ",
        "い",
        "う",
        "え",
        "お",
        "か",
        "き",
        "く",
        "け",
        "こ",
        "さ",
        "し",
        "す",
        "せ",
        "そ",
        "た",
        "ち",
        "つ",
        "て",
        "と",
        "な",
        "に",
        "ぬ",
        "ね",
        "の",
        "は",
        "ひ",
        "ふ",
        "へ",
        "ほ",
        "ま",
        "み",
        "む",
        "め",
        "も",
        "や",
        "ゆ",
        "よ",
        "わ",
        "を",
        "が",
        "ぎ",
        "ぐ",
        "げ",
        "ご",
        "ざ",
        "じ",
        "ず",
        "ぜ",
        "ぞ",
        "だ",
        "ぢ",
        "づ",
        "で",
        "ど",
        "ば",
        "び",
        "ぶ",
        "べ",
        "ぼ"
      ],
      scale: 5,
      pika: [],
      marginRight: 5,
      marginBottom: 5,
      shuffledLeft: [],
      shuffledName: [],
      shuffledLike: [],
      next: true,
      confirm: false
    };
  },
  methods: {
    setStyle() {
      const wrapper = document.querySelector(".wrapper");
      wrapper.style.width =
        this.scale * 200 + this.scale * this.marginRight + "px";
      wrapper.style.height =
        this.scale * 100 + this.scale * this.marginBottom + "px";
      console.log("setstyle");
    },
    leftsShuffle() {
      for (let i = 0; i < this.scale ** 2; i++) {
        let j = Math.floor(Math.random() * this.lefts.length);
        this.shuffledLeft.push(this.lefts[j]);
      }
    },
    namesShuffle() {
      for (let i = 0; i < this.scale ** 2; i++) {
        let j = Math.floor(Math.random() * this.names.length);
        this.shuffledName.push(this.names[j]);
      }
    },
    likesShuffle() {
      for (let i = 0; i < this.scale ** 2; i++) {
        let j = Math.floor(Math.random() * this.likes.length);
        this.shuffledLike.push(this.likes[j]);
      }
    },
    updateLefts() {
      for (let i = 0; i < this.scale ** 2; i++) {
        let leftLetters = document.querySelectorAll(".leftLetter");
        let name = document.querySelectorAll(".name");
        let like = document.querySelectorAll(".like");
        let j = Math.floor(Math.random() * this.lefts.length);
        let k = Math.floor(Math.random() * this.names.length);
        let l = Math.floor(Math.random() * this.likes.length);
        leftLetters[i].textContent = this.lefts[j];
        name[i].textContent = this.names[k];
        like[i].textContent = this.likes[l];
      }
      console.log("updateLefts");
    },
    toNext() {
      this.next = !this.next;
    },
    check() {
      this.confirm = true;
    },
    start() {
      this.confirm = false;
    },
    reset() {
      this.confirm = false;
      console.log("clicked!!!!!!!!!!!!!!!!!!!!!!!!!");
      console.log(this.scale ** 2);
    },
    see(e) {
      e.check = true;
      console.log(e);
    },
    pusher() {
      this.pika = [];
      for (let i = 0; i < this.scale ** 2; i++) {
        let prop = {
          check: false,
          num: i
        };
        this.pika.push(prop);
      }
      console.log("pusher");
    },
    deleter() {
      for (let i = 0; i < this.scale ** 2; i++) {
        this.pika[i].check = false;
        console.log(this.pika[i].check);
      }
    }
  },
  created() {
    this.check();
    this.leftsShuffle();
    this.namesShuffle();
    this.likesShuffle();
    console.log("created!");
    console.log(this.pika);
    console.log(this.scale ** 2);
    console.log(this.pika.length);
    console.log("created!");
  },
  mounted() {
    console.log("mounted");
    this.setStyle();
    this.pusher();
    console.log(this.scale ** 2);
    console.log(this.pika.length);

    console.log("mounted");
  },
  updated() {
    console.log("updated!");
    console.log(this.scale ** 2);
    console.log(this.pika.length);
    console.log("updated!");
  },
  watch: {
    next() {
      console.log("watch-next");
      this.setStyle();
      this.pusher();
      this.updateLefts();
      console.log("watch-next");
    },
    scale() {
      console.log("watch-scale");
      console.log(this.scale ** 2);
      this.check();
      this.pusher();
      this.setStyle();
      this.updateLefts();

      console.log("watch-scale");
    }
  }
};
</script>

<style>
* {
  margin: 0;
  user-select: none;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #4f6c8a;
  padding-top: 10px;
  background-color: rgb(240, 255, 251);
  height: 770px;
}
p {
  margin: 0;
}
.btnWrapper {
  display: flex;
  justify-content: space-between;
  width: 250px;
  margin: 0 auto;
}
.btn {
  width: 70px;
  height: 30px;
  line-height: 29px;
  margin: 0 auto;
  font-size: 20px;
  border-radius: 2px;
  margin-top: 10px;
  background-color: rgb(191, 255, 208);
  box-shadow: 0 2px 0 rgb(121, 230, 193);
}
.btn:hover {
  cursor: pointer;
  opacity: 0.8;
}
.btn:active {
  position: relative;
  top: 2px;
  box-shadow: none;
}
input {
  height: 18px;
  width: 18px;
  margin-left: 10px;
}
input:hover {
  cursor: pointer;
}
span {
  font-size: 20px;
}
.wrapper {
  width: 615px;
  height: 315px;
  margin: 0 auto;
  padding-top: 5px;
  padding-left: 5px;
  background-color: rgb(220, 255, 245);
  display: flex;
  flex-wrap: wrap;
  align-content: flex-start;
}
.content {
  width: 178px;
  height: 98px;
  margin-right: 5px;
  margin-bottom: 5px;
  padding-left: 20px;
  background-color: rgb(211, 255, 223);

  border: 1px solid rgb(121, 230, 193);
  display: flex;
  justify-content: space-between;
}
.content:hover {
  cursor: pointer;
}
.check {
  background-color: #4f6c8a;
  border: 1px solid rgb(72, 155, 255);
}
.see {
  background-color: rgb(211, 255, 223);

  border: 1px solid rgb(121, 230, 193);
}
.name,
.like {
  font-size: 23px;
}
.info {
  padding: 30px 0;
}
.left {
  font-size: 17px;
  line-height: 50px;
  margin-top: 25px;
  padding: 0;
}
.right {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
.rightWrapper {
  width: 130px;
  display: flex;
  justify-content: center;
}
</style>
