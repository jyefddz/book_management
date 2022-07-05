<template>
    <div>
        <div>
            <input type="text" placeholder="搜索-书本名称" autofocus v-model.trim="bookname" @keydown.enter="enter">
            <button @click="getBooks">查看全部图书</button>
        </div>
        <br>
        <table border="1" cellspacing="0" cellpadding="6" width="50%" height="100%">
            <tr style="background-color: #ccc">
                <th>序号</th>
                <th>书名</th>
                <th>作者</th>
                <th>出版商</th>
                <th>操作</th>
            </tr>
            <tr v-for="item in books" :key="item.id">
                <td>{{ item.id }}</td>
                <td>{{ item.bookname }}</td>
                <td>{{ item.author }}</td>
                <td>{{ item.publisher }}</td>
                <td>
                    <a href="javascript:;" @click="delFn(item.id)">删除</a>
                    <a href="javascript:;" @click="detFn(item.id)">详情</a>
                </td>
            </tr>
        </table>
    </div>

</template>

<script>
export default {
    data() {
        return {
            books: [],
            bookname: '',
            searchbook: ''
        }
    },
    mounted() {
        this.$axios.get('/api/getbooks').then((res) => {
            console.log(res);
            this.books = res.data.data
        })
    },
    methods: {
        getBooks() {
            this.$axios({
                url: "/api/getbooks",
            }).then((res) => {
                console.log(res);
                this.books = res.data.data
            })

        },
        enter() {
            this.$axios({
                url: '/api/getbooks',
                params: {
                    bookname: this.bookname
                }
            }).then((res) => {
                console.log(res);
                this.books = res.data.data
            })
        },
        delFn(id) {
            this.$axios({
                method: 'delete',
                url: '/api/delbook',
                params: {
                    id: id
                }
            }).then((res) => {
                console.log(res);
                console.log(id);
                location.replace('http://localhost:8081/')
            })
        },
        detFn(id) {
            this.$axios({
                url: '/api/getbooks',
                params: {
                    id: id
                }
            }).then((res) => {
                const info = res.data.data && res.data.data[0];
                alert(
                    `作者：${info.author}; 出版社：${info.publisher}; 书名：${info.bookname}`
                );
            })
        }
    }
}
</script>

<style>
</style>