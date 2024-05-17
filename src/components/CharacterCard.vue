<template>
  <div class="card">
    <div class="card-img">
      <img :src="character.image" alt="Secret Service Rick">
    </div>
    <div class="card-text">
      <div class="section">
        <h2 class="hovered">{{character.name}}</h2>
        <div class="status"><span class="status-icon" :class="character.status"></span> {{character.status}} - {{character.species}}</div>
      </div>
      <div class="section">
        <span class="text-title">Last known location:</span>
        <span class="hovered">{{character.location.name}}</span>
      </div>
      <div class="section">
        <span class="text-title">First seen in:</span>
        <span class="hovered">{{character.firstEpisodeName}}</span></div>
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
      color: rgb(245, 245, 245);
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

      .status {
        display: flex;
        -webkit-box-align: center;
        align-items: center;
        text-transform: capitalize;
        font-size: 16px;
        font-weight: 500;
        color: rgb(255, 255, 255);

        .status-icon {
          height: 0.5rem;
          width: 0.5rem;
          margin-right: 0.375rem;
          font-size: 16px;
          border-radius: 50%;

          &.Alive {
            background: rgb(85, 204, 68);
          }

          &.Dead {
            background: rgb(214, 61, 46);
          }

          &.unknown {
            background: rgb(220, 220, 46);
          }
        }
      }

      .text-title {
        color: rgb(158, 158, 158);
        font-size: 16px;
        font-weight: 500;
      }

      h2 {
        margin: 0;
        padding: 0;
        font-weight: 800;
        line-height: 1.1
      }

      .hovered:hover {
        color: rgb(255, 152, 0);
        cursor: pointer;
      }
    }
  }
</style>
