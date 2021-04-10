<template>
  <b-row>
    <b-col cols="12">
      <h2>
        编辑图书
        <router-link to="/book-list">图书列表</router-link>
      </h2>
      <b-jumbotron>
        <template slot="header">
          {{book.title}}
        </template>
        <template slot="lead">
          ISBN: {{book.isbn}}<br><br>
          作者: {{book.author}}<br><br>
          内容简介: {{book.description}}<br><br>
          出版年: {{book.published_year}}<br><br>
          出版社: {{book.publisher}}<br>
        </template>
        <hr class="my-4">
        <p>
          更新日期: {{book.updated_date}}
        </p>
        <b-btn variant="success" @click.stop="editbook(book._id)">编辑</b-btn>
        <b-btn variant="danger" @click.stop="deletebook(book._id)">删除</b-btn>
      </b-jumbotron>
    </b-col>
  </b-row>
</template>

<script>

import axios from 'axios'

export default {
  name: 'ShowBook',
  data () {
    return {
      book: []
    }
  },
  created () {
    axios.get(`http://222.198.139.97:3003/book/` + this.$route.params.id)
    .then(response => {
      this.book = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  },
  methods: {
    editbook (bookid) {
      this.$router.push({
        name: 'EditBook',
        params: { id: bookid }
      })
    },
    deletebook (bookid) {
      axios.delete('http://222.198.139.97:3003/book/' + bookid)
      .then((result) => {
        this.$router.push({
          name: 'BookList'
        })
      })
      .catch(e => {
        this.errors.push(e)
      })
    }
  }
}
</script>

<style>
  .jumbotron {
    padding: 2rem;
  }
</style>
