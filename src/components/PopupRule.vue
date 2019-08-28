<template>
  <div class="wrapper-popup" :class="getClassPopup">
    <div class="rule">
      <h3>Luật chơi</h3>
      <p>
        NewGame
        <br /> 1. Nhập FinalScore
        <br /> 2. Click NewGame
        <br />Roll Dice
        <br /> 1. Nếu xoay trúng số 1 -> Mất hết điểm hiện tại -> Đổi lượt chơi.
        <br /> 2. Nếu xoay ok -> Cộng dồn vào điểm hiện tại.
        <br />Hold
        <br /> 1. Cộng dồn điểm hiện tại vào điểm của người chơi
        <br /> 2. Điểm của người chơi >= FinalScore -> Winner
        <br /> 3. Chưa đủ điểm -> Đổi lượt chơi
        <br />
      </p>
      <button class="confirm" @click="confirm()">Đã hiểu</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "popup-rule",
  props: {
    isOpenPopup: { type: Boolean, default: false }
  },
  data() {
    return {};
  },
  methods: {
    confirm() {
      this.$emit("handleConfirm");
    }
  },
  computed: {
    getClassPopup() {
      return {
        "open-popup": this.isOpenPopup
      };
    }
  }
};
</script>

<style>
.wrapper-popup {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.4);
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
}
.wrapper-popup.open-popup {
  opacity: 1;
  visibility: visible;
}
.rule {
  width: 350px;
  padding: 20px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(1.2);
  background-color: #fff;
  font-family: Arial;
  transition: all 0.3s ease;
}
.open-popup.rule {
  transform: translate(-50%, -50%) scale(1);
}
h3 {
  margin-bottom: 10px;
}
.rule .confirm {
  margin-top: 20px;
  cursor: pointer;
  padding: 8px 15px;
  border: 2px solid #333;
  background-color: #fff;
  transition: all 0.3s ease;
}
.rule .confirm:hover {
  color: #fff;
  background-color: #000;
}
</style>