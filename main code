from flask import Flask, request, redirect

import string
import random

app = Flask(__name__)

url_mapping = {}

def generate_short_code(length=6):
    characters = string.ascii_letters + string.digits
    return ''.join(random.choices(characters, k=length))

@app.route('/', methods=['GET', 'POST'])
def home():
    if request.method == 'POST':
        original_url = request.form['url']
        short_code = generate_short_code()
        url_mapping[short_code] = original_url
        short_url = request.host_url + short_code
        return f'Short URL: <a href="{short_url}">{short_url}</a>'
    return '''
        <h2>URL Shortener</h2>
        <form method="post">
            <input type="text" name="url" placeholder="Enter URL" required>
            <input type="submit" value="Shorten">
        </form>
    '''

@app.route('/<short_code>')
def redirect_url(short_code):
    original_url = url_mapping.get(short_code)
    if original_url:
        return redirect(original_url)
    return '<h3>Invalid short URL!</h3>', 404

# THIS IS VERY IMPORTANT TO START THE SERVER
if __name__ == '__main__':
    app.run(debug=True)
