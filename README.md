# website.github.io
<!DOCTYPE html>
<html>
<head>
    <title>Asset Inventory</title>
</head>
<body>
    <h1>Asset Inventory</h1>
    <form method="post">
        Asset Tag: <input name="asset_tag"><br>
        Hostname: <input name="hostname"><br>
        IP Address: <input name="ip_address"><br>
        Location: <input name="location"><br>
        Floor: <input name="floor"><br>
        Remarks: <input name="remarks"><br>
        <button type="submit">Add Asset</button>
    </form>
    <table border="1">
        <tr>
            <th>Sl.no</th>
            <th>Asset Tag</th>
            <th>Hostname</th>
            <th>IP Address</th>
            <th>Location</th>
            <th>Floor</th>
            <th>Remarks</th>
        </tr>
        {% for asset in assets %}
        <tr>
            <td>{{ asset[0] }}</td>
            <td>{{ asset[1] }}</td>
            <td>{{ asset[2] }}</td>
            <td>{{ asset[3] }}</td>
            <td>{{ asset[4] }}</td>
            <td>{{ asset[5] }}</td>
            <td>{{ asset[6] }}</td>
        </tr>
        {% endfor %}
    </table>
</body>
</html>
