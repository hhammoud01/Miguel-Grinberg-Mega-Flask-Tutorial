import json
import requests, uuid
from flask_babel import _
from app import app

def translate(text, source_language, dest_language):
    if 'MS_TRANSLATOR_KEY' not in app.config or \
            not app.config['MS_TRANSLATOR_KEY']:
        return _('Error: the translation service is not configured')

    headers = {
        'Ocp-Apim-Subscription-Key': app.config['MS_TRANSLATOR_KEY'],
        'Ocp-Apim-Subscription-Region': 'eastus'
#       'Content-type': 'application/json'
#        'X-ClientTraceId': str(uuid.uuid4())
    }

    body = [{
        'text': text
    }]

    endpoint = 'https://api.cognitive.microsofttranslator.com'
    path = '/translate?api-version=3.0'
    params = '&from={}&to={}'.format(source_language, dest_language)

    url = endpoint + path + params

    r = requests.post(url, headers=headers, json=body)

    if r.status_code != 200:
        return _('Error: the translation service failed')
    return json.loads(r.content.decode('utf-8-sig'))[0]['translations'][0]['text']
