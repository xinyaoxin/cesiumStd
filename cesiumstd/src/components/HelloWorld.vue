<template>
  <div class="hello">
    <p @click="del">回退</p>
    <p>使用G6</p>
    <div id="mountNode" class="wrap">
      <div class="right">
        <ul>
          数据
          <li
            v-for="item in getDta"
            :key="item.id"
            @click="addArgument(item)"
          >
            {{ item.num }}
          </li>
        </ul>
      </div>
      <ul class="paramsLeft">
        参数：
        <li v-for="item in calcuNum" :key="item" @click="delNum(item)">
          {{ item.num }}
        </li>
      </ul>
      <ul class="cal">
        <li value="+" @click="addFn($event)">+</li>
        <li @click="addFn($event)">-</li>
        <li @click="addFn($event)">*</li>
        <li @click="addFn($event)">/</li>
      </ul>
    </div>
    <button @click="confirm">确定</button>
  </div>
</template>

<script>
import G6 from "@antv/g6";
export default {
  name: "HelloWorld",
  data() {
    return {
      calcuNum: [],
      getDta: [
        {
          id: 0,
          num: 99,
        },
        {
          id: 1,
          num: 88,
        },
        {
          id: 2,
          num: 92,
        },
        {
          id: 3,
          num: 83,
        },
        {
          id: 4,
          num: 99,
        },
        {
          id: 5,
          num: 88,
        },
      ],
      graph: null,
      res: "",
      data: {
        // 点集
        nodes: [],
        // 边集
        edges: [
          // 表示一条从 node1 节点连接到 node2 节点的边
          // {
          //   source: "node1",
          //   target: "node2",
          // },
        ],
      },
      addedNodeCount: 7,
      x: 100,
      y: 100,
    };
  },
  mounted() {
    this.initGraph();
  },
  methods: {
    initGraph() {
      this.graph = new G6.Graph({
        container: "mountNode", // 画布宽高
        width: 900,
        height: 200,
        modes: {
          default: ["drag-canvas", "zoom-canvas", "drag-node",'create-edge'],
        },
      }); // 读取数据
      this.graph.data(this.data); // 渲染图
      this.graph.render();
    },
    addArgument(arg) {
      console.log('arg',arg.num);
      const addArgument = arg.num;
      const model = {
        id: `node${this.addedNodeCount}`,
        label: addArgument,
        type: "circle",
        x: `${this.x}`,
        y: 150,
      };
      
      this.graph.addItem("node", model);
      this.addedNodeCount++;
      this.x += 100;
      console.log(this.graph.cfg.nodes);
    },

    addFn($event) {
      const symbol = $event.target.outerText;
      this.res += symbol;
      const model = {
        id: `node${this.addedNodeCount}`,
        label: symbol,
        type: "rect",
        x: `${this.x}`,
        y: 150,
      };
      const modelEdge = {
        source: `node${this.addedNodeCount - 1}`,
        target: `node${this.addedNodeCount}`,
      };
      this.graph.addItem("node", model);
      this.addedNodeCount++;
      this.x += 100;
      console.log(this.graph.cfg.nodes);
    },
    del() {
      this.addedNodeCount--;
      const item = this.graph.findById(`node${this.addedNodeCount}`);
      this.graph.removeItem(item);
      if (this.x <= 100) {
        this.x = 100;
      } else {
        this.x -= 100;
        const arr = this.res.split("");
        console.log(this.res);
      }
    },
    addNum($event) {
      const num = $event;
      this.calcuNum.push(num);
      console.log(11, this.calcuNum);
    },
    confirm(){
      console.log(this.graph.save());
    }
  },
};
</script>

<style scoped>
.cal {
  float: left;
}

li {
  width: 20px;
  border: 1px solid;
  line-height: 20px;
  list-style: none;
  float: right;
  margin-right: 20px;
  font-size: 20px;
}
.wrap {
  border: 1px solid;
}
</style>
