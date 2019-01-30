<template>
    <div id="noti">
      <p>태거니 바보</p>
    </div>
</template>

<script>
export default {
  name: 'Notification'
}
</script>

<style scoped>
  #noti{
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    position: absolute;
    margin-left: auto;
    margin-right: auto;
    left: 0;
    right: 0;
    margin-top: 3vh;
    border-radius: 5px;
    height: 10vh;
    width: 90vw;
    background-color: #FFFFFF;
    box-shadow: 0 23px 87px 0px rgba(255,255,255,0.24);
  }p{
    font-size: 30px;
     }
</style>
