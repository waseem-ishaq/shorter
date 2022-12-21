<template>
  <div >
    <v-row>
      <v-col ><h1>Make your url shorter</h1></v-col>
      
    </v-row>
    <v-row>
      <v-col><hr></v-col>
    </v-row>
    <v-form>
      <v-container class="ma-4">
        <v-row>
          <v-col cols="12">
            <v-text-field
              v-model="userUrl"
              outlined
              clearable
              label="Enter your long url"
              type="text"
              ><template v-slot:append-outer>
                <v-btn @click="apiCall(userUrl)"> convert </v-btn>
              </template>
            </v-text-field>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
    <v-form>
      <v-container class="ma-4">
        <v-row>
          <v-col cols="12">
            <v-text-field
              v-model="shorterUrl"
              outlined
              type="text"
              placeholder="Your Short URL"
              />
          </v-col>
        </v-row>
      </v-container>
    </v-form>

   
    
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  data: () => ({ userUrl: "",
  shorterUrl:''
 }),
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
      }).then((response) => response.json().then((data)=>{
        console.log(data.short_url);
        this.shorterUrl=data.short_url;
      }));
    },
  },
};
</script>
<!-- FE5qNilsGxXqNaoOe2h0Iduz6kP1Bj4765AMqHHlKFbPLteG2DCtDutIHYoa -->
