<template>
    <div>
        <div>
            <input type="text" placeholder="书名" v-model.trim="bookObj.bookname">
        </div>
        <div>
            <input type="text" placeholder="作者" v-model.trim="bookObj.author">
        </div>
        <div>
            <input type="text" placeholder="出版社" v-model.trim="bookObj.publisher">
        </div>
        <button>发布</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            bookObj: { // 参数名提前和后台的参数名对上-发送请求就不用再次对接了
                bookname: "",
                author: "",
                publisher: ""
            },
            books: [],
        }
    },
    Mounted() {
        this.$axios({
            url: '/api/addbook',
            method: 'POST',
            data: {
                appkey: "7250d3eb-18e1-41bc-8bb2-11483665535a",
                ...this.bookObj
            }
        }).then((res) => {
            alert('添加成功')
            this.bookObj.bookname = ''
            this.bookObj.author = ''
            this.bookObj.publisher = ''
        })

    }



}
</script>

<style>
</style>