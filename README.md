import os
from google.oauth2 import service_account
from googleapiclient.discovery import build

# Replace 'YOUR_SERVICE_ACCOUNT_JSON_FILE.json' with your service account JSON file
credentials = service_account.Credentials.from_service_account_file('YOUR_SERVICE_ACCOUNT_JSON_FILE.json', scopes=['https://www.googleapis.com/auth/drive.file'])

# Create a Google Slides service
slides_service = build('slides', 'v1', credentials=credentials)

# Create a presentation
presentation = slides_service.presentations().create().execute()
presentation_id = presentation['presentationId']

# Add a title slide
title_slide = slides_service.presentations().pages().create(presentationId=presentation_id, body={'title': 'The Night Watch'}).execute()

# Add content slides as needed

# Print the link to the created presentation
presentation_link = f'https://docs.google.com/presentation/d/{presentation_id}/edit'
print(f'Your presentation on "The Night Watch" is ready: {presentation_link}')
