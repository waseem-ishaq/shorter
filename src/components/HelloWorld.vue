<template>
  <div class="mainDiv">
    <div class="header">
      <img class="mainImage" src="../assets/images/shortUrl.png" alt="" />
    </div>
    <section class="white sec mx-auto pa-6">
      <div>
        <h1><b>Paste the URL to be shortened</b></h1>
      </div>
      <div>
        <v-form>
          <v-container class="ma-4">
            <div>
              <div cols="12">
                <v-text-field
                  v-model="userUrl"
                  outlined
                  clearable
                  label="Enter your long url"
                  type="text"
                >
                </v-text-field>
              </div>
              <div>
                <v-btn class="con-btn info" @click="apiCall(userUrl)">
                  convert
                </v-btn>
              </div>
              <div class="ma-4">
                <b
                  >ShortURL.at is a free tool to shorten a URL or reduce a link
                  Use our URL Shortener to create a shortened link making it
                  easy to remember
                </b>
              </div>
            </div>
          </v-container>
        </v-form>
      </div>
    </section>

    <section class="white ma-4 sec mx-auto pa-6">
      <div>
        <h1><b>Short URL</b></h1>
      </div>
      <v-form>
        <v-container class="ma-4">
          <div>
            <div cols="12">
              <v-text-field
                v-model="shorterUrl"
                outlined
                type="text"
                placeholder="Your Short URL"
              />
            </div>
          </div>
          <div><b>Long URL: </b>{{ this.userUrl }}</div>
        </v-container>
      </v-form>
    </section>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  data: () => ({ userUrl: "", shorterUrl: "" }),
  methods: {
    apiCall(userUrl) {
      const url = new URL("https://t.ly/api/v1/link/shorten");
      const params = {
        api_token:
          "FE5qNilsGxXqNaoOe2h0Iduz6kP1Bj4765AMqHHlKFbPLteG2DCtDutIHYoa",
      };
      Object.keys(params).forEach((key) =>
        url.searchParams.append(key, params[key])
      );
      const headers = {
        "Content-Type": "application/json",
        Accept: "application/json",
      };
      let body = {
        long_url: userUrl,
        domain: "",
        include_qr_code: false,
      };
      fetch(url, {
        method: "POST",
        headers,
        body: JSON.stringify(body),
      }).then((response) =>
        response.json().then((data) => {
          console.log(data.short_url);
          this.shorterUrl = data.short_url;
        })
      );
    },
  },
};
</script>
<!-- FE5qNilsGxXqNaoOe2h0Iduz6kP1Bj4765AMqHHlKFbPLteG2DCtDutIHYoa -->
<style scoped>
.mainDiv {
  height: 100vh;
  background-color: #f9f9f9;
}
.mainImage {
  width: 250px;
}
.sec {
  width: 50%;
}
</style>
