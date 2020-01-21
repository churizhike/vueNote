1.对象、数组深拷贝

    1.简单类型数据拷贝
        对象：Object.assign()
        数组：slice(start,end) 复制返回选定的原素到新数组
    2.值为undefined、function、symbol时不可以，其他类型都可
        对象/数组：JSON.parse(JSON.stringfy(obj))
    3.全类型
        对象/数组：
        function deepCopy(obj) {
            var result = Array.isArray(obj) ? [] : {};
            for (var key in obj) {
                if (obj.hasOwnProperty(key)) {
                    if (typeof obj[key] === 'object' && obj[key]!==null) {
                        result[key] = deepCopy(obj[key]);   //递归复制
                    } else {
                        result[key] = obj[key]; 
                    }
                }
            }
            return result;
        }
    