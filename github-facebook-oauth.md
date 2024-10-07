# Flask ব্যবহার করে GitHub এবং Facebook OAuth ইন্টিগ্রেশন করতে পারেন। নিচে প্রতিটি প্ল্যাটফর্মের জন্য ধাপগুলো দেওয়া হলো:

### GitHub OAuth ইন্টিগ্রেশন

#### ধাপ ১: GitHub OAuth Credentials তৈরি করুন
1. **GitHub Developer Settings** এ যান: GitHub Developer Settings।
2. **OAuth Apps** এ যান এবং **New OAuth App** ক্লিক করুন।
3. প্রয়োজনীয় তথ্য পূরণ করুন:
    - **Application name**: আপনার অ্যাপের নাম।
    - **Homepage URL**: আপনার অ্যাপের হোমপেজ URL।
    - **Authorization callback URL**: `http://localhost:5000/github/authorize` (বা আপনার অ্যাপের রিডাইরেক্ট URI)।
4. **Register application** ক্লিক করুন।
5. **Client ID** এবং **Client Secret** নোট করুন।

#### ধাপ ২: Flask অ্যাপ্লিকেশন সেটআপ করুন
```python
from flask import Flask, url_for, redirect, session, render_template
from authlib.integrations.flask_client import OAuth
import os

app = Flask(__name__)
app.secret_key = os.getenv('SECRET_KEY', 'default_secret_key')

oauth = OAuth(app)
github = oauth.register(
    name='github',
    client_id=os.getenv('GITHUB_CLIENT_ID'),
    client_secret=os.getenv('GITHUB_CLIENT_SECRET'),
    access_token_url='https://github.com/login/oauth/access_token',
    authorize_url='https://github.com/login/oauth/authorize',
    api_base_url='https://api.github.com/',
    client_kwargs={'scope': 'user:email'},
)

@app.route('/')
def home():
    email = dict(session).get('email', None)
    return render_template('home.html', email=email)

@app.route('/login/github')
def login_github():
    redirect_uri = url_for('authorize_github', _external=True)
    return github.authorize_redirect(redirect_uri)

@app.route('/github/authorize')
def authorize_github():
    token = github.authorize_access_token()
    resp = github.get('user')
    user_info = resp.json()
    session['email'] = user_info['email']
    return redirect('/')

@app.route('/logout')
def logout():
    session.pop('email', None)
    return redirect('/')

if __name__ == '__main__':
    app.run(debug=True)
```

### Facebook OAuth ইন্টিগ্রেশন

#### ধাপ ১: Facebook OAuth Credentials তৈরি করুন
1. **Facebook for Developers** এ যান: Facebook for Developers।
2. **My Apps** এ যান এবং **Create App** ক্লিক করুন।
3. **App Type** নির্বাচন করুন এবং **Create App ID** ক্লিক করুন।
4. **Settings** > **Basic** এ যান এবং **Add Platform** এ ক্লিক করে **Website** নির্বাচন করুন।
5. **Site URL** এ আপনার অ্যাপের URL দিন।
6. **Facebook Login** > **Settings** এ যান এবং **Valid OAuth Redirect URIs** এ `http://localhost:5000/facebook/authorize` যোগ করুন।
7. **App ID** এবং **App Secret** নোট করুন।

#### ধাপ ২: Flask অ্যাপ্লিকেশন সেটআপ করুন
```python
from flask import Flask, url_for, redirect, session, render_template
from authlib.integrations.flask_client import OAuth
import os

app = Flask(__name__)
app.secret_key = os.getenv('SECRET_KEY', 'default_secret_key')

oauth = OAuth(app)
facebook = oauth.register(
    name='facebook',
    client_id=os.getenv('FACEBOOK_CLIENT_ID'),
    client_secret=os.getenv('FACEBOOK_CLIENT_SECRET'),
    access_token_url='https://graph.facebook.com/v10.0/oauth/access_token',
    authorize_url='https://www.facebook.com/v10.0/dialog/oauth',
    api_base_url='https://graph.facebook.com/v10.0/',
    client_kwargs={'scope': 'email'},
)

@app.route('/')
def home():
    email = dict(session).get('email', None)
    return render_template('home.html', email=email)

@app.route('/login/facebook')
def login_facebook():
    redirect_uri = url_for('authorize_facebook', _external=True)
    return facebook.authorize_redirect(redirect_uri)

@app.route('/facebook/authorize')
def authorize_facebook():
    token = facebook.authorize_access_token()
    resp = facebook.get('me?fields=id,name,email')
    user_info = resp.json()
    session['email'] = user_info['email']
    return redirect('/')

@app.route('/logout')
def logout():
    session.pop('email', None)
    return redirect('/')

if __name__ == '__main__':
    app.run(debug=True)
```

### পরিবেশ ভেরিয়েবল সেটআপ
`.env` ফাইলে নিচের মতো করে সেট করুন:
```
SECRET_KEY=your_generated_secret_key
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret
FACEBOOK_CLIENT_ID=your_facebook_client_id
FACEBOOK_CLIENT_SECRET=your_facebook_client_secret
```

এখন আপনার অ্যাপ্লিকেশনটি চালু করুন এবং GitHub ও Facebook OAuth ব্যবহার করে লগইন করতে পারবেন। যদি কোনো প্রশ্ন থাকে বা কোনো অংশে সাহায্য প্রয়োজন হয়, আমাকে জানাতে পারেন!

Source: Conversation with Copilot, 10/7/2024
(1) github.com. https://github.com/pamfilos/invenio-authlib/tree/510b115a323c89e5334a9669bbf47932d2b8a00b/invenio_authlib%2Fconfig.py.
(2) github.com. https://github.com/OpenMined/private-identity-server/tree/0995ec03640ab23081ab83f015cc62d99649238a/server%2Fapp%2Fextensions.py.
(3) github.com. https://github.com/sballarati/python-flask-oauth/tree/ee2e2cb82e9e6eaf51396fcf8a441fe689cf5d0b/hello.py.
