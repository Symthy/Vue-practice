<template>
  <div>
    <table>
      <tr v-for="(rowDataArray, rowNum) in existingDataArray" :key="rowNum">
        <td v-for="(data, colNum) in rowDataArray" :key="data">
          <input v-model="rowDataArray[rowNum][colNum]" type="text" />
        </td>
        <td>
          <input type="checkbox" />
        </td>
      </tr>
      <tr v-for="(rowDataArray, rowNum) in newDataArray" :key="rowNum">
        <td v-for="(data, colNum) in rowDataArray" :key="data">
          <input v-model="newDataArray[rowNum][colNum]" type="text" />
        </td>
        <td>
          <button @click="removeNewData(colNum)">削除</button>
        </td>
      </tr>
    </table>

    <button @click="addNewData">追加(仮)</button>

    <button @click="registerData">登録(仮)</button>
  </div>
</template>

<script>
export default {
  data() {
    existingDataArray: [];
    newDataArray: [];
  },
  methods: {
    addNewData() {
      const datas = [];
      newDataArray.push(datas);
    },
    removeNewData(rowNum) {
      newDataArray.splice(rowNum);
    },
    registerData() {
      const allDataArray = existingDataArray.concat(newDataArray);
    },
  },
};
</script>
