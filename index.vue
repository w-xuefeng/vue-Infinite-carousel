 <template>
    <div class="wrap" :style="{'height': height + 'px', 'width': width + 'px'}">
      <div class="train" :style="{'width': width * items.length + 'px', 'transition': 'transform ' + time + 'ms', 'margin-left': '-' + width + 'px', 'transform': 'translateX(' + change + ')'}" ref="train">
        <div v-for="(item, i) in items" :key="i" :style="{'height': height + 'px', 'width': width + 'px','background-image': 'url(' + item + ')'}" class="imgBack"></div>
      </div>
      <div class="btn prev" @click="prev()">
        <svg class="icon" style="width: 1em; height: 1em;vertical-align: middle;fill: #FFF;overflow: hidden;" viewBox="0 0 1024 1024" version="1.1"  xmlns="http://www.w3.org/2000/svg" p-id="1488">
          <path d="M385.5019999999999 512.004L754.9959999999999 142.53499999999997c17.935999999999993-17.962000000000007 17.93699999999999-47.064-2.1316282072803006e-14-65s-47.01299999999999-17.936999999999994-64.949 2.1316282072803006e-14l-434.49399999999997 434.46900000000016L690.0470000000003 946.448c17.936000000000007 17.961999999999993 47.013000000000005 17.961999999999982 64.949-2.1316282072803006e-14 17.936999999999994-17.937000000000005 17.935999999999993-47.038-2.1316282072803006e-14-64.975l-369.49300000000017-369.4689999999999z m0 0z" p-id="1489">
          </path>
        </svg>
      </div>
      <div class="btn next" @click="next()">
        <svg class="icon" style="width: 1em; height: 1em;vertical-align: middle;fill: #FFF;overflow: hidden; transform: scaleX(-1);" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1488">
          <path d="M385.5019999999999 512.004L754.9959999999999 142.53499999999997c17.935999999999993-17.962000000000007 17.93699999999999-47.064-2.1316282072803006e-14-65s-47.01299999999999-17.936999999999994-64.949 2.1316282072803006e-14l-434.49399999999997 434.46900000000016L690.0470000000003 946.448c17.936000000000007 17.961999999999993 47.013000000000005 17.961999999999982 64.949-2.1316282072803006e-14 17.936999999999994-17.937000000000005 17.935999999999993-47.038-2.1316282072803006e-14-64.975l-369.49300000000017-369.4689999999999z m0 0z" p-id="1489">
          </path>
        </svg>
      </div>
    </div>
</template>
<script>
export default {
  name: 'InfiniteCarousel',
  data () {
    return {
      img: true,
      height: 300,
      width: 500,      
      time: 300,
      items: [
        'https://raw.githubusercontent.com/w-xuefeng/imgChange/master/img/bg52.jpg',
        'https://raw.githubusercontent.com/w-xuefeng/imgChange/master/img/bg78.jpg',
        'https://raw.githubusercontent.com/w-xuefeng/imgChange/master/img/bg79.jpg',
        'https://raw.githubusercontent.com/w-xuefeng/imgChange/master/img/bg81.jpg',
        'https://raw.githubusercontent.com/w-xuefeng/imgChange/master/img/bg82.jpg'
      ],      
      change: 0,
      index: 0
    }
  },
  methods: {
    prev () {
      this.index++;
      this.change = `${this.width * this.index}px`;
      setTimeout(() => {
        this.$refs.train.style.marginLeft = `${-this.width * (this.index + 1)}px`;
        this.items.unshift(this.items.pop());
      }, this.time);
      
    },
    next () {
      this.index--;
      this.change = `${this.width * this.index}px`;
      setTimeout(() => {
        this.$refs.train.style.marginLeft = `${-this.width * (this.index + 1)}px`;
        this.items.push(this.items.shift());
      }, this.time);
    },
  }
}
</script>
<style>
*{
  margin: 0;
  padding: 0;
}
</style>
<style scoped>
.wrap {
  width: 100%;
  position: relative;
  overflow: hidden;
}
.train {
  display: flex;
  align-items: center;  
}
.imgBack {
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}
.btn {
  padding: 10px;
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0,0,0,0.05);
  transition: all 800ms;
  cursor: pointer;
}
.btn:hover {
  background: rgba(0,0,0,0.65);
}
.prev {
  left: 0;
}
.next {
  right: 0;
}
</style>
