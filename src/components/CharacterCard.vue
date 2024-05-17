<template>
  <div class="card">
    <div class="card-img">
      <img :src="character.image" alt="Secret Service Rick">
    </div>
    <div class="card-text">
      <div class="section">
        <h2>{{character.name}}</h2>
        <span class="status"><span class="status-icon"></span> {{character.status}} - {{character.species}}</span>
      </div>
      <div class="section">
        <span class="text-gray">Last known location:</span>
        <p>{{character.location.name}}</p>
      </div>
      <div class="section">
        <span class="text-gray">First seen in:</span>
        <p>{{character.firstEpisodeName}}</p></div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'CharacterCard',
    props: {
      character: {}
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .card {
    font: 112.5% / 1.625 -apple-system, 'BlinkMacSystemFont', 'Segoe UI', 'Roboto', 'Helvetica', 'Arial', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';
    width: 600px;
    height: 220px;
    display: flex;
    overflow: hidden;
    background: rgb(60, 62, 68);
    border-radius: 0.5rem;
    margin: 0.75rem;
    box-shadow: rgba(0, 0, 0, 0.1) 0 4px 6px -1px, rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;

    .card-img {
      flex: 2 1 0;
      width: 100%;

      img {
        width: 100%;
        height: 100%;
        margin: 0;
        opacity: 1;
        transition: opacity 0.5s ease 0s;
        object-position: center center;
        object-fit: cover;
      }
    }

    .card-text {
      flex: 3 1 0;
      position: relative;
      padding: 0.75rem;
      color: rgb(255, 255, 255);
      display: flex;
      flex-direction: column;
      text-align: start;

      .section {
        flex: 1 1 0;
        display: flex;
        flex-direction: column;
        -webkit-box-pack: center;
        justify-content: center;

        &:first-child {
          -webkit-box-pack: start;
          justify-content: flex-start;
        }

        &:last-child {
          -webkit-box-pack: end;
          justify-content: flex-end;
        }
      }

      h2 {
        margin: 0;
        padding: 0;
        font-weight: 800;
        line-height: 1.1
      }
    }
  }
</style>
