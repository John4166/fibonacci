# fibonacci
###递归方法
````
function fibonacci(n){
    var result=0;
    if(n<=0){throw new Error("输入的数不能小于0")}
    if(n<3){
        return 1;
    }
    if(n>=3){
        result=fibonacci(n-1)+fibonacci(n-2)
    }
    return result;
}

```
以上有不足之处：
会重复计算函数值，比如fibonacci(5)会分解成fibonacci(4)+fibonacci(3)，fibonacci(4)又会分解成fibonacci(3)+fibonacci(2)，fibonacci(4)重复了
,最简单的办法就是记录下已经计算过的值：
改进方法：
````
function fibonacci2(){
    var arr=[1,1];
    function calc(n){
        if(n<1){throw new Error("输入的数不能小于0")}
        if(n<3){
            return arr[n-1];
        }
        if(arr[n-1]!=undefined){
            return arr[n-1];//记录已有的数组数据
        }
        var data=calc(n-1)+calc(n-2);
        arr[n-1] = data;
        return data;
    }
    return calc;
}
````

###不递归的方法
````
function getFibonacci(n) {
    var fibarr = [];
    var i = 0;
    while(i < n) {
        if(i <= 1) {
            fibarr.push(i);
        } else {
            fibarr.push(fibarr[i - 1] + fibarr[i - 2])
        }
        i++;
    }
    return fibarr;
}

````

###generator生成器生成
循环输出55以内的数值，跟结果不太一样
````
function* fibonacci5() {
    let [prev, curr] = [0, 1];
    for (;;) {
        [prev, curr] = [curr, prev + curr];
        yield curr;
    }
}
for (let curr of fibonacci5()) {
    if (curr>55) break;
    console.log(curr);
}
````