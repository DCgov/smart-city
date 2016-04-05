---
layout: page
permalink: /inventory.html
title: Inventory (in progress)
---

<p><input id="inventoryTableFilter" type="text" placeholder="search..."></p>

<div id="inventoryTable"></div>

<p><em><a href="https://docs.google.com/spreadsheets/d/1m9pukHIAACMIy2ESAvhhB6sEYw-E1L7wyK3WdPCJpk0/pub?gid=0&single=true&output=csv" target="_blank">download data</a></em></p>

{% raw %}
<script id="inventoryTable_template" type="text/html">
  <table>
  <thead>
    <tr><th class="tHeader">Name</th><th class="tHeader">Lead</th><th class="tHeader">Description</th></tr>
  </thead>
  <tbody>
      {{#rows}}
        <tr>
          <td>{{projectname}}</td>
          <td>{{leadorganization}}</td>
          <td>{{projectdescription}}</td>
        </tr>
      {{/rows}}
  </tbody>
  </table>
</script>
{% endraw %}

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/tabletop.js/1.4.3/tabletop.min.js"></script>
<script type="text/javascript" src="/assets/js/sheetsee.js"></script>
<script type="text/javascript">
    var key = '1m9pukHIAACMIy2ESAvhhB6sEYw-E1L7wyK3WdPCJpk0'
    var sheet = 'Published to Website'
    document.addEventListener('DOMContentLoaded', function() {
        Tabletop.init({ key: key, wanted: [sheet], callback: showInfo, prettyColumnNames: false })
    })

    function showInfo(data) {
        console.log(data[sheet].all())
        var tableOptions = {
            data: data[sheet].all(),
            pagination: 10,
            tableDiv: '#inventoryTable',
            filterDiv: '#inventoryTableFilter'
        }

        Sheetsee.makeTable(tableOptions)
        Sheetsee.initiateTableFilter(tableOptions)
    }
</script>