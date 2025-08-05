# website.github.io
from flask import Flask, render_template, request, redirect
import sqlite3

app = Flask(__name__)

def init_db():
    conn = sqlite3.connect('assets.db')
    c = conn.cursor()
    c.execute('''
        CREATE TABLE IF NOT EXISTS assets (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            asset_tag TEXT,
            hostname TEXT,
            ip_address TEXT,
            location TEXT,
            floor TEXT,
            remarks TEXT
        )
    ''')
    conn.commit()
    conn.close()

@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        asset_tag = request.form['asset_tag']
        hostname = request.form['hostname']
        ip_address = request.form['ip_address']
        location = request.form['location']
        floor = request.form['floor']
        remarks = request.form['remarks']
        
        conn = sqlite3.connect('assets.db')
        c = conn.cursor()
        c.execute("INSERT INTO assets (asset_tag, hostname, ip_address, location, floor, remarks) VALUES (?, ?, ?, ?, ?, ?)",
                  (asset_tag, hostname, ip_address, location, floor, remarks))
        conn.commit()
        conn.close()
        return redirect('/')
    else:
        conn = sqlite3.connect('assets.db')
        c = conn.cursor()
        c.execute("SELECT * FROM assets")
        assets = c.fetchall()
        conn.close()
        return render_template('index.html', assets=assets)

if __name__ == '__main__':
    init_db()
    app.run(debug=True)
