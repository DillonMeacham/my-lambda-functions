import json
import os
import boto3

def lambda_handler(event, context):
    # Retrieve the email address from the environment variable
    email_address = os.environ.get('EMAIL_ADDRESS')

    # Create an instance of the Amazon SES service
    ses = boto3.client('ses')

    # Customize the email content
    subject = 'Resume Access Notification'
    message = 'Someone accessed your resume.'

    # Set the parameters for sending the email
    params = {
        'Destination': {
            'ToAddresses': [email_address]
        },
        'Message': {
            'Subject': {
                'Data': subject
            },
            'Body': {
                'Text': {
                    'Data': message
                }
            }
        },
        'Source': email_address
    }

    try:
        # Send the email using the SES service
        response = ses.send_email(**params)

        # Return a response indicating success
        return {
            'statusCode': 200,
            'body': json.dumps({
                'message': 'Email notification sent successfully.',
                'messageId': response['MessageId']
            })
        }
    except Exception as e:
        # Return an error response if there's an issue sending the email
        return {
            'statusCode': 500,
            'body': json.dumps({
                'error': 'Error sending email notification: ' + str(e)
            })
        }
