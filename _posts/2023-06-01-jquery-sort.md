---
title: JQuery Sort
comments: true
layout: base
description: Try simple table with JQuery Sort
permalink: /frontend/jquery
tags: [javascript]
---
<head>
    <!-- JQuery -->
    <script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-3.5.1.js"></script>
    <script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.13.4/js/jquery.dataTables.min.js"></script>
    <!-- Bootstrap -->
    <script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.13.4/js/dataTables.bootstrap5.min.js"></script>
    <style>
        #flaskTable th:first-child {
            width: 75px;
        }
        #flaskTable td:not(:first-child) {
          width: 150px;
        }
    </style>

</head>

<table id="flaskTable" class="table table-striped nowrap" style="width:100%">
    <thead id="flaskHead">
        <tr>
            <th>acous</th>
            <th>artist</th>
            <th>bpm</th>
            <th>dance</th>
            <th>duration</th>
            <th>energy</th>
            <th>id</th>
            <th>live</th>
            <th>loud</th>
            <th>popular</th>
            <th>speech</th>
            <th>title</th>
            <th>genre</th>
            <th>valence</th>
            <th>year</th>
        </tr>
    </thead>
    <tbody id="flaskBody"></tbody>
</table>

<script>
  $(document).ready(function() {
    fetch('https://playourshiny.duckdns.org/songdatabase', { mode: 'cors' })
    .then(response => {
      if (!response.ok) {
        throw new Error('API response failed');
      }
      return response.json();
    })
    .then(data => {
      for (const row of data) {
        $('#flaskBody').append('<tr><td>' + 
            row.acousticness + '</td><td>' +
            row.artist + '</td><td>' +
            row.bpm + '</td><td>' +
            row.danceability + '</td><td>' +
            row.duration + '</td><td>' +
            row.energy + '</td><td>' +
            row.id + '</td><td>' +
            row.liveness + '</td><td>' +
            row.loudness + '</td><td>' +
            row.popularity + '</td><td>' +
            row.speechiness + '</td><td>' +
            row.title + '</td><td>' +
            row.top_genre + '</td><td>' +
            row.valence + '</td><td>' +
            row.year + '</td></tr>');
      }
      $('#flaskTable').DataTable();
    })
    .catch(error => {
      console.error('Error:', error);
    })
  });
</script>


