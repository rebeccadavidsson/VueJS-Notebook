<template>

    <div class="wrapper">
        <BackgroundTitle title="ThoughtBook" location="right"/>
        <div class="inner">
            <Title title="Your Personal ThoughtBook" />
            <Notes />
        </div>
    </div>
  
</template>

<script>

import BackgroundTitle from './subComponents/BackgroundTitle';
import Title from './subComponents/Title';
import Notes from './subComponents/Notes';

export default {
  name: 'Notebook',
  components: {
      BackgroundTitle,
      Title,
      Notes,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.wrapper {
    background-color: #979aa982;
    width: 60%;
    height: calc(90% - 5em);
    margin: 0 auto;
    border-radius: 7px;
    box-shadow: 0 15px 25px rgb(0 0 0 / 60%);
}
.inner {
    color: white;
    padding: 4em 5em;
    height: calc(100% - 8em);
}

</style>
