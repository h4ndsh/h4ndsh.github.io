# Bug Bounty


<style>

    .table-container {
      width: 100%;
      overflow: hidden;
      border: 0px!important;
    }

     .table-container table {
      width: 100%;
      border-collapse: collapse;
      background-color: transparent!important;
      border: 0px!important;
    }
     .table-container thead {
      border: 0px!important;
      background-color: transparent!important;
      padding-bottom: 50px;
      font-size: 24px;
    }

     .table-container th,  .table-container td {
      padding: 20px;
      text-align: center;
      border: 0px!important;
    }

    .table-container tr {
      margin-bottom: 20px!important;
      text-align: center !important;
    }

    .table-container th {
      color: #fff;
    }

    .table-container td {
      border: 0;
    }

    .low, .medium, .high, .critical {
      color: #fff;
      font-weight: bold;
      display: inline;
      padding: 5px;
      border-radius: 5px;
      text-transform: uppercase; /* Adicionado para transformar o texto em maiúsculas */
      margin: 2px; /* Adicionado para adicionar um pequeno espaçamento entre as tags */
    }

    .low {
      background-color: #007FFF;
    }

    .medium {
      background-color: #ffd150;
    }

    .high {
      background-color: #FF8000;
    }

    .critical {
      background-color: #b30000;
    }
    thead tr:first-child th{ 
      padding-bottom: 25px !important;
      text-transform: uppercase;
    }
  </style>

# Vulnerabilities Discovered and Reported


<div class="table-container">
    <table>
      <thead>
        <tr>
          <th>entity</th>
          <th>vulnerability</th>
          <th>Year</th>
          <th>Severity</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><a href="https://www.airc.pt" target="_blank">AIRC</a></td>
          <td>DOM-based Injection</td>
          <td>2024</td>
          <td class="high">high</td>
        </tr>
        <tr>
          <td><a href="https://anmp.pt" target="_blank">ANMP</a></td>
          <td>Email Exposure</td>
          <td>2023</td>
          <td class="critical">CRITICAL</td>
        </tr>
        <tr>
          <td><a href="https://fefal.pt" target="_blank">FEFAL</a></td>
          <td>Storaged XSS</td>
          <td>2023</td>
          <td class="high">high</td>
        </tr>
        <tr>
          <td><a href="https://fefal.pt" target="_blank">FEFAL</a></td>
          <td>Exposed web configs</td>
          <td>2023</td>
          <td class="critical">CRITICAL</td>
        </tr>
         <tr>
          <td><a href="https://fefal.pt" target="_blank">FEFAL</a></td>
          <td>Reflected XSS</td>
          <td>2023</td>
          <td class="medium">MEDIUM</td>
        </tr>
        <tr>
          <td><a href="https://fefal.pt" target="_blank">FEFAL</a></td>
          <td>Directory Listing</td>
          <td>2023</td>
          <td class="low">Low</td>
        </tr>
        <tr>
          <td><a href="https://fefal.pt" target="_blank">FEFAL</a></td>
          <td>Unrestricted File Upload</td>
          <td>2023</td>
          <td class="high">high</td>
        </tr>
        <tr>
          <td><a href="https://fefal.pt" target="_blank">FEFAL</a></td>
          <td>Sensitive Data Exposure</td>
          <td>2023</td>
          <td class="high">high</td>
        </tr>
        <tr>
          <td><a href="https://fefal.pt" target="_blank">FEFAL</a></td>
          <td>IDOR</td>
          <td>2023</td>
          <td class="critical">critical</td>
        </tr>
      </tbody>
    </table>
  </div>
