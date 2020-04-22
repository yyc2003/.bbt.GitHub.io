## Welcome to GitHub Pages

<script src="https://cdn.bootcss.com/vue/2.6.11/vue.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/leancloud-storage@4.5.3/dist/av-min.js"></script>
<script type="text/javascript">
    var {
        Query
    } = AV;
    AV.init({
        appId: "Llrd2wR7cCPRlcXlwcOpMMEM-MdYXbMMI", //你的 leancloud 应用 id （设置-应用keys-AppID）
        appKey: "iaVHEe9QBwkdk1bQwEbl7yvE", //你的 leancloud 应用 AppKey （设置-应用keys-AppKey）
    });


    var query = new AV.Query('content');
    
    var app = new Vue({
        el: '#app',
        data: {
            page: 0,
            count: 0,
            contents: []
        },
        methods: {
            loadMore: function(event) {
                getData(++this.page);
            }
        }
    })
    
    function urlToLink(str) {
        var re = /(http|ftp|https):\/\/[\w-]+(.[\w-]+)+([\w-.,@?^=%&:/~+#]*[\w-\@?^=%&/~+#])?/g;;
    
        str = str.replace(re, function(website) {
            return "<a href='" + website + "' target='_blank'> <i class='iconfont icon-lianjie-copy'></i>链接 </a>";
        });
        return str;
    }
    
    function getData(page = 0) {
        query.descending('createdAt').skip(page * 20).limit(20).find().then(function(results) {
            if (results.length == 0) {
                alert('之前没 b 过了')
            } else {
                let resC = results;
                reqData = false;
                resC.forEach((i) => {
                    let dateTmp = new Date(i.createdAt);
                    i.attributes.time = `${dateTmp.getFullYear()}-${(dateTmp.getMonth() + 1) < 10 ? ('0' + (dateTmp.getMonth()+1)) : dateTmp.getMonth()+1}-${(dateTmp.getDate() + 1) < 10 ? ('0' + dateTmp.getDate()) : dateTmp.getDate()} ${(dateTmp.getHours() + 1) <= 10 ? ('0' + dateTmp.getHours()) : dateTmp.getHours()}:${(dateTmp.getMinutes() + 1) <= 10 ? ('0' + dateTmp.getMinutes()) : dateTmp.getMinutes()}`;
                    i.attributes.content = "<span>" + urlToLink(i.attributes.content) + "</span>";
                    app.contents.push(i);
                })
            }
    
        }, function(error) {});
    }
    
    getData(0);
    
    query.count().then(function(count) {
        app.count = count;
    }, function(error) {});

</script>

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/yyc2003/bbt.GitHub.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
