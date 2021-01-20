<template>
  <div>
    <table>
      <tr>
        <th>item1</th>
        <th>item2</th>
        <th>item3</th>
        <th>item4</th>
        <th>item5</th>
        <th>option</th>
      </tr>
      <tr v-for="(rowDataArray, rowNum) in dataArray" :key="`ext-row-${rowNum}`">
        <td v-for="(data, colNum) in rowDataArray" :key="`ext-col-${colNum}`">
          <input v-model="dataArray[rowNum][colNum]" type="text" />
        </td>
        <td>
          <input type="checkbox" />
        </td>
      </tr>
      <tr v-for="(rowNewDataArray, rowNum) in newDataArray" :key="`new-${rowNum}`">
        <td v-for="(data, colNum) in rowNewDataArray" :key="`new-col-${colNum}`">
          <input v-model="newDataArray[rowNum][colNum]" type="text" />
        </td>
        <td>
          <button @click="removeNewData(rowNum)">削除</button>
        </td>
      </tr>
    </table>

    <button @click="addNewData">追加</button>
    <form method="POST" @submit="registerData">
      <button>登録</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dataArray: [],
      newDataArray: [],
    };
  },
  methods: {
    addNewData() {
      const datas = Array(5).fill("");
      this.newDataArray.push(datas);
    },
    removeNewData(rowNum) {
      this.newDataArray.splice(rowNum, 1);
    },
    registerData() {
      const is_ok = confirm("Register?");
      if (!is_ok) {
        event.preventDefault();
        return;
      }
      this.dataArray = this.dataArray.concat(this.newDataArray);
      this.newDataArray = [];
      event.preventDefault(); // 本来はデータ送信
    },
  },
};
</script>
