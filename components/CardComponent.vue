<template>
  <v-card height="20vh" ripple @click="edit(memo.id)">
    <!-- タイトル -->
    <v-card-title class="headline">
      {{ memo.data.title }}
    </v-card-title>
    <!-- 削除ボタン -->
    <div class="ma-2" style="position: absolute; bottom: 0; right: 0">
      <v-btn icon color="red" @click="remove(memo.id)">
        <v-icon>mdi-trash-can-outline</v-icon>
      </v-btn>
    </div>
    <!-- サブタイトル(時刻を表示) -->
    <div style="position: absolute; bottom: 0">
      <v-card-subtitle>{{ memo.data.timestamp }}</v-card-subtitle>
    </div>
  </v-card>
</template>

<script>
export default {
  // 親から渡された値
  props: { memo: { type: Object, required: true } },
  // 計算した値をとる変数
  computed: {
    memos() {
      // store/memos.js/listを取得
      return this.$store.state.memos.list
    },
  },
  // 関数定義
  methods: {
    edit(id) {
      const path = '/' + id
      this.$router.push(path)
    },
    remove(id) {
      if (confirm('削除しますか？')) {
        // store/memos.js/removeDBを実行
        this.$store.dispatch('memos/removeDB', id)
      }
    },
  },
}
</script>
