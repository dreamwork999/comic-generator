<template>
  <section class="content-wrapper" style="min-height: 960px;">
    <section class="content-header">
      <h1>Books</h1>
    </section>

    <section class="content">
      <div class="row">
        <div class="col-xs-12">
          <div class="box">
            <div class="box-header with-border">
              <h3 class="box-title">View</h3>
            </div>

            <div class="box-body">
              <!-- <back-buttton></back-buttton> -->
              <router-link
                v-if="item.book_id > 0&&$can('character_access')"
                :to="{ name: 'characters.index',params: { id: item.book_id}}"
                class="btn btn-default btn-sm"
              >
                <span class="glyphicon glyphicon-chevron-left"></span> Back to all Characters
              </router-link>
            </div>

            <div class="box-body">
              <div class="row" v-if="loading">
                <div class="col-xs-4 col-xs-offset-4">
                  <div class="alert text-center">
                    <i class="fa fa-spin fa-refresh"></i> Loading
                  </div>
                </div>
              </div>
              <div class="row" v-if="!loading">
                <div class="col-xs-6">
                  <table class="table table-bordered table-striped">
                    <tbody>
                      <tr>
                        <th>#</th>
                        <td>{{ item.id }}</td>
                      </tr>
                      <tr>
                        <th>Name</th>
                        <td>{{ item.name }}</td>
                      </tr>
                      <tr>
                        <th>Image</th>
                        <td>
                          <img :src="item.thumb_url" width="160" class="my-image" />
                        </td>
                      </tr>
                      <tr>
                        <th>Check Layers</th>
                        <td>
                          <router-link
                            :to="{ name: 'characters.layer_check', params: { id: item.id } }"
                            class="btn btn-primary"
                          >Check</router-link>
                        </td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </section>
</template>


<script>
import { mapGetters, mapActions } from "vuex";

export default {
  data() {
    return {
      // Code...
    };
  },
  created() {
    this.fetchData(this.$route.params.id);
  },
  destroyed() {
    this.resetState();
  },
  computed: {
    ...mapGetters("CharactersSingle", ["item", "loading"])
  },
  watch: {
    "$route.params.id": function() {
      this.resetState();
      this.fetchData(this.$route.params.id);
    }
  },
  methods: {
    ...mapActions("CharactersSingle", ["fetchData", "resetState"])
  }
};
</script>


<style scoped>
</style>
