
<template>
  <div class="touch">
    <br>
    <v-row justify="center" align="center">
      <v-main style="padding-bottom: 30px">
        <section id="main">
          <v-img

            :src="blog"
          />
        </section>
      </v-main>
    </v-row>
    <!--
    <v-row justify="center" align="center" style="padding-bottom: 30px">
       <AppButton

        @click="saveImg"
      >
        <i class="fas fa-download" /> บันทึกภาพ
      </AppButton>
    </v-row>
    -->
    <v-row justify="center" align="center" style="padding-bottom: 30px">
      <AppButtonShare

        @click="share"
      >
        <i class="fab fa-facebook-square" /> แชร์ผ่านเฟสบุค
      </AppButtonShare>
    </v-row>
    <v-row justify="center" align="center" style="padding-bottom: 30px">
      <AppButtonLine

        @click="saveImg"
      >
        <i class="fab fa-line" /> ดาวน์โหลดการ์ด
      </AppButtonLine>
    </v-row>
    <v-row justify="center" align="center" style="padding-bottom: 20px">
      <AppButtonLine

        @click="shareLine"
      >
        <i class="far fa-paper-plane" /> ชวนเพื่อนมาลงชื่อ
      </AppButtonLine>
    </v-row>
    <v-row justify="center" align="center">
      <AppButton

        @click="back"
      >
        <i class="fas fa-home" /> กลับหน้าหลัก
      </AppButton>
    </v-row>
  </div>
</template>
<script>
import AppButton from '../components/Buttonsubmit'
import AppButtonShare from '../components/Buttonshare'
import AppButtonLine from '../components/ButtonLine'

export default {
  components: {
    AppButton,
    AppButtonShare,
    AppButtonLine
  },
  data () {
    return {
      blog: null,
      name: '',
      profile: null,
      img: null
    }
  },

  head () {
    return {
      title: 'ลงชื่อเพื่อ ร่วมเป็น 1 ในผู้สถาปนา ในวันวิสาขบูชาโลก ออนไลน์ ครั้งที่1',
      meta: [
        { hid: 'description', property: 'description', content: `${this.$store.state.user.user.title} ร่วมจองโคมจุดประทีปออนไลน์ ในวันมาฆบูชา` },
        { hid: 'og:title', property: 'og:title', content: `${this.$store.state.user.user.title} ร่วมจองโคมจุดประทีปออนไลน์ ในวันมาฆบูชา` },
        { hid: 'og:description', property: 'og:description', content: `${this.$store.state.user.user.title} ร่วมจองโคมจุดประทีปออนไลน์ ในวันมาฆบูชา` },
        { hid: 'og:url', property: 'og:url', content: 'https://master.d35xisgv6y1ahr.amplifyapp.com' },
        { hid: 'og:image', property: 'og:image', content: this.$store.state.user.user.coverImage },

        { hid: 'og:type', property: 'og:type', content: 'website' }
      ]
    }
  },
  computed: {
    coverImg () {
      if (this.name) {
        return `https://res.cloudinary.com/dda7dxqvr/image/upload/w_340,c_fit,l_text:sarabun.ttf_48:${this.name},y_220,co_rgb:3E2914/indexcard3.jpg`
        // return `https://res.cloudinary.com/dz4zph4bl/image/upload/w_2520,c_fit,l_text:Arial_260:${this.name},g_south,y_700,co_rgb:FFFFFF/card-social_vqioai.jpg`
      } else {
        return 'https://res.cloudinary.com/dda7dxqvr/image/upload/v1621888519/cardindex.jpg'
      }
    },
    cname () {
      return this.name
    },
    user () {
      return this.$store.state.user.user
    }
  },
  async mounted () {
    // eslint-disable-next-line no-undef
    await liff.init({ liffId: '1656023598-jbmRQA1P' }).then(() => {
      // eslint-disable-next-line no-undef
      if (liff.isLoggedIn()) {
        this.getUserProfile()
      // eslint-disable-next-line no-undef
      } else {
      // eslint-disable-next-line no-undef
      //  liff.login({ redirectUri: 'https://master.d1xnc86zjtxdwi.amplifyapp.com/' })
      }
    })

    const id = this.$route.params.id
    this.name = id
    const response = `https://res.cloudinary.com/dda7dxqvr/image/upload/w_340,c_fit,l_text:sarabun.ttf_48:${this.name},y_220,co_rgb:3E2914/indexcard3.jpg`
    this.img = response
    this.blog = this.$store.state.user.user.coverImage
    // eslint-disable-next-line no-undef
  },
  methods: {
    async getUserProfile () {
      // eslint-disable-next-line no-undef
      const profile = await liff.getProfile()
      this.profile = profile
    },
    back () {
      // console.log(this.src)
      this.$router.replace('/')
    },
    share () {
      // eslint-disable-next-line no-undef
      // eslint-disable-next-line no-undef
      liff.openWindow({
        url: `https://www.facebook.com/sharer/sharer.php?u=${this.$store.state.user.user.coverImage}`,
        external: true
      })
      // return window.location.href('https://www.facebook.com/dialog/share?app_id=1093024467833550&display=popup&href=https://master.d35xisgv6y1ahr.amplifyapp.com/card&redirect_uri=https://master.d35xisgv6y1ahr.amplifyapp.com/card')
      // https://www.facebook.com/sharer/sharer.php?u=https://master.d35xisgv6y1ahr.amplifyapp.com
      // https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Fmaster.d35xisgv6y1ahr.amplifyapp.com%2Fcard&amp;src=sdkpreparse
    },
    saveImg () {
      // eslint-disable-next-line no-undef
      // liff.openWindow({
      //   url: this.$store.state.user.user.coverImage,
      //   external: true
      // })
      this.downloadImage(this.$store.state.user.user.coverImage)
    },
    async sharel () {
      // eslint-disable-next-line no-undef
      if (liff.getContext().type !== 'none') {
        // eslint-disable-next-line no-undef
        await liff.sendMessages([

          {
            type: 'flex',
            altText: 'ลงชื่อเพื่อร่วมเป็น 1 ในผู้สถาปนา ในวันวิสาขบูชาโลก ออนไลน์ ครั้งที่ 1',
            contents: {
              type: 'bubble',
              body: {
                type: 'box',
                layout: 'vertical',
                spacing: 'md',
                contents: [
                  {
                    type: 'text',
                    text: 'ลงชื่อเพื่อร่วมเป็น 1 ในผู้สถาปนา ในวันวิสาขบูชาโลก ออนไลน์ ครั้งที่ 1',
                    weight: 'bold',
                    size: 'xl',
                    margin: 'xs',
                    wrap: true,
                    style: 'normal',
                    decoration: 'none',
                    align: 'center',
                    offsetBottom: 'none'
                  },
                  {
                    type: 'image',
                    url: this.user.coverImage,
                    position: 'relative',
                    offsetTop: '-20px',
                    align: 'center',
                    size: 'full',
                    aspectRatio: '2:3',
                    aspectMode: 'fit',
                    animated: true
                  }
                ]
              },
              footer: {
                type: 'box',
                layout: 'vertical',
                spacing: 'sm',
                contents: [],
                flex: 0

              }
            }
          }

        ])
      }
    },
    async sendMessage () {
      // eslint-disable-next-line no-console
      // console.log(this.$store.state.user.user.coverImage)
      // eslint-disable-next-line no-undef
      try {
        // eslint-disable-next-line no-undef
        await liff.sendMessages([
          {
            type: 'sticker',
            stickerId: 2,
            packageId: 1

          },
          {
            type: 'image',
            originalContentUrl: this.$store.state.user.user.coverImage,
            previewImageUrl: this.$store.state.user.user.coverImage
          }
        ])
        alert('ส่งการ์ดไปให้คุณแล้ว')
        // eslint-disable-next-line no-undef
        // liff.closeWindow()
      } catch (e) {
        // eslint-disable-next-line no-console
        console.log(e)
        // eslint-disable-next-line no-undef
        const [majorVer, minorVer, patchVer] = (liff.getLineVersion() || '').split('.')

        if (minorVer === undefined) {
          alert('Message was canceled in external browser')
          return
        }

        if (parseInt(majorVer) >= 10 && parseInt(minorVer) >= 10 && parseInt(patchVer) > 0) {
          alert('Message was canceled in LINE app')
        }
      }
    },
    async shareLine () {
      // eslint-disable-next-line no-undef
      // eslint-disable-next-line no-undef
      const result = await liff.shareTargetPicker([
        {
          type: 'flex',
          altText: 'ลงชื่อเพื่อ ร่วมเป็น 1 ในผู้สถาปนา ในวันวิสาขบูชาโลก ออนไลน์ ครั้งที่1',
          contents: {
            type: 'bubble',
            body: {
              type: 'box',
              layout: 'vertical',
              spacing: 'md',
              contents: [
                {
                  type: 'text',
                  text: 'ลงชื่อเพื่อ ร่วมเป็น 1 ในผู้สถาปนา ในวันวิสาขบูชาโลก ออนไลน์ ครั้งที่1',
                  weight: 'bold',
                  size: 'xl',
                  margin: 'xs',
                  wrap: true,
                  style: 'normal',
                  decoration: 'none',
                  align: 'center',
                  offsetBottom: 'none'
                },
                {
                  type: 'image',
                  url: this.$store.state.user.user.coverImage,
                  position: 'relative',
                  offsetTop: '-20px',
                  align: 'center',
                  size: 'full',
                  aspectRatio: '2:3',
                  aspectMode: 'fit',
                  animated: true,
                  action: {
                    type: 'uri',
                    label: 'action',
                    uri: this.$store.state.user.user.coverImage
                  }
                }
              ]
            },
            footer: {
              type: 'box',
              layout: 'vertical',
              spacing: 'xs',
              contents: [
                {
                  type: 'button',
                  action: {
                    type: 'uri',
                    label: 'ลงชื่อเพื่อ ร่วมเป็น 1 ในผู้สถาปนา',
                    uri: 'https://lin.ee/4FpzwqY'
                  },
                  style: 'primary',
                  height: 'md'
                }
              ]

            }
          }
        }
      ])
      if (result) {
        alert('ส่งข้อความไปหาเพื่อนของคุณแล้ว!')
      } else {
        // eslint-disable-next-line no-undef
        const [majorVer, minorVer, patchVer] = (liff.getLineVersion() || '').split('.')

        if (minorVer === undefined) {
          alert('ShareTargetPicker was canceled in external browser')
          return
        }

        if (parseInt(majorVer) >= 10 && parseInt(minorVer) >= 10 && parseInt(patchVer) > 0) {
          alert('ShareTargetPicker was canceled in LINE app')
        }
      }
    },
    async downloadImage (imageSrc) {
      const image = await fetch(imageSrc)
      const imageBlog = await image.blob()
      const imageURL = URL.createObjectURL(imageBlog)

      const link = document.createElement('a')
      link.href = imageURL
      link.download = 'vesakaWorldOnline-1st'
      document.body.appendChild(link)
      link.click()
      document.body.removeChild(link)
    }
  }
}
</script>
<style scoped>
.scroll-touch {
  -webkit-overflow-scrolling: auto; /* Lets it scroll lazy */
}
 .touch {
   overflow-x: hidden;
  overflow-y: scroll; /* has to be scroll, not auto */
  -webkit-overflow-scrolling: touch;
  z-index: 999;
}
</style>
