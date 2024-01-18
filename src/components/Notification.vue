<template>

</template>
<style></style>
<script>
import {createDiscreteApi} from "naive-ui";

const {message, notification, dialog, loadingBar} = createDiscreteApi([
  "message",
  "dialog",
  "notification",
  "loadingBar",
]);
window.$message = message;
window.$dialog = dialog;
window.$notification = notification;
window.$loadingBar = loadingBar;


</script>
