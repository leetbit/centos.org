---
title: Mirror List
is_hidden: false
layout: default
---
<h1>List of CentOS Mirrors</h1>
<p class="lead"> 
CentOS welcomes new mirror sites. If you are considering setting up a
public mirror site for CentOS, <a href="http://wiki.centos.org/HowTos/CreatePublicMirrors">please follow the mirror guidelines</a> to make
sure that your mirror is consistent with the other mirror sites.
If you're searching for mirrors providing AltArch content (like ppc64,ppc64le,aarch64,armfhp) please use <a href="/download/altarch-mirrors/"> this link </a><br>
To check the status of a mirror, please visit <a href="http://mirror-status.centos.org/"> mirror-status.centos.org </a>
</p>

<div id="CSVTable"></div>
<script type="text/javascript" src="/assets/js/jquery.csvToTable2.js"></script>
<script type="text/javascript" src="/assets/js/jquery.tablesorter.min.js"></script>
<link rel="stylesheet" type="text/css" href="/assets/csvtable-look.css">

<script>
$('#CSVTable').CSVToTable('/download/full-mirrorlist.csv', 
    { 
       startLine: 1,
       //['Location', 'Region', 'Sponsor', 'HomePage', 'HTTP location', 'FTP Location', 'Rsync Location']
       headers: [
       'Location', 
       'Region', 
       {label:'Sponsor' , items:[2 , 3]}, 
       {label:'HomePage' , hidden:true}, 
       'HTTP location', 
       'FTP Location', 
       'Rsync Location'
       ],
       itemMerger: function(header , items) {
          var outItem = [];
          console.log(items);
          for(var i in header.items){
            var item = header.items[i];
            outItem.push(items[item]);
          }
          if(header.label = 'Sponsor'){
             console.log(outItem);
             return '<a href="' + outItem[1] + '" target="_blank">' + outItem[0] + '</a>';
          }else return outItem.join(' ');
      },
      preRenderItem: function(headerLabel , item) {
        if(item == '') return '';
        switch (headerLabel) {
          case 'HTTP location':
          case 'FTP Location':
          case 'Rsync Location':
              item = item.replace(/"/gi , '');
              return '<a href="' + item + '" target="_blank">' + item + '</a>'; 
          default:
              return item;
        }
      }
    }
).bind("loadComplete",function() { 
  $('#CSVTable').find('TABLE').tablesorter({
    widgets: ['zebra', 'filter'],
    widgetOptions: {
      uitheme: "bootstrap"
    },
    textExtraction: function(node) {  
        // extract data from markup and return it  
        return $(node).text();
    } 
  });

});;
</script>

<noscript>
  <div id
