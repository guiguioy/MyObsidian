# react vue 父子组件调用

## 总结

### react

**子组件调用父组件函数方法**

```html
<!--父组件-->
<Children getInfo="{getInfo}" />
<!--子组件-->
<span onClick="{param.getInfo}">调用父组件函数</span>
```

**父组件调用子组件函数方法**

```javascript
<!--父组件-->
const childRef=useRef();
childRef.current.getInfo();
<Children ref={childRef} />
<!--子组件-->
useImperativeHandle(ref, () => ({
    getInfo:()=>{
        //需要处理的数据
    }
}))
```

### vue

**子组件调用父组件函数方法**

```html
<!--父组件-->
<children @parentMethod="macSelect"></children>
<!--子组件-->
<span onClick="{param.getInfo}">调用父组件函数</span>
```

**父组件调用子组件函数方法**

```javascript
<!--父组件-->
this.$refs.child1.handleParentClick("ssss");
```

## react hook

### 子组件调用父组件函数方法

**父组件**

```js
let Father = () => {
	let getInfo = () => {
		// DODO:
	};
	return () => {
		<div>
			<Children getInfo={getInfo} />
		</div>;
	};
};
```

**子组件**

```
    let Children=(param)=>{
        return ()=>{
            <div>
                <span onClick={param.getInfo}>调用父组件函数</span>
            </div>
        }
    }
```

### 父组件调用子组件函数方法

**父组件**

```
    import {useRef} from 'react'
    let Father=()=>{
        const childRef=useRef();
        let onClick=()=>{
            childRef.current.getInfo();
        }
        return ()=>{
            <div>
                <Children ref={childRef} />
                <span onClick={onClick}>调用子组件函数</span>
            </div>
        }
    }
```

**子组件**

```
    import {useImperativeHandle,forwardRef} from 'react'
    let Children=(ref)=>{
        useImperativeHandle(ref, () => ({
            getInfo:()=>{
                //需要处理的数据
            }
        }))
        return ()=>{
            <div></div>
        }
    }
    Children = forwardRef(Children);

    // 使用hook React.FC不需要↑上面这句
    const SortWBSTree: React.FC<any> = (props: any) => {
    }
    export default React.memo(SortWBSTree);
    // 可以不用forwardRef
```

## vue

### 子组件调用父组件函数方法

**父组件**

```
    <template>
          <div class="wrapper">
                <cp_action @parentMethod="macSelect"></cp_action>
          </div>
    </template>
    <script>
    import ../components/action  //引入子组件
    export default{
        components:{
            cp_action
        },
        method:{
            macSelect(){
                //方法体
                alert(123)；
            }
        }
    }
    </script>
```

**子组件**

```
    let Children=(param)=>{
        return ()=>{
            <div>
                <span onClick={param.getInfo}>调用父组件函数</span>
            </div>
        }
    }

```

### 父组件调用子组件函数方法

**父组件**

```
    <template>
        <div>
            <button v-on:click="clickParent">点击</button>
            <child1 ref="child1"></child1>
        </div>
    </template>

    <script>
        import Child1 from './child1';
        export default {
            name: "parent",
            components: {
                child1: Child1
            },
            methods: {
                clickParent() {
                    // this.$refs.child1.$emit('click-child', "high");
                    this.$refs.child1.handleParentClick("ssss");
                }
            }
        }
    </script>
```

**子组件**

```
    <script>
        export default {
            name: "child1",
            props: "msg",
            methods: {
                handleParentClick(e) {
                }
            }
        }
    </script>
```
