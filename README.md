- 👋 Hi, I’m @PrashantVishal82
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
PrashantVishal82/PrashantVishal82 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

# Gmail account credentials
GMAIL_USER = 'prashantvishal82@gmail.com'
GMAIL_APP_PASSWORD = 'dwcm zyvo xuwl ldrt'  # App password, not your actual Gmail password

# List of recipients
recipients = ['prashant_psfin2006@gmail.com']

# Email content
subject = "Your Bulk Email Subject"
body = """\
Hi there,

This is a test email sent from Python!

Best,
Your Name
"""

def send_bulk_emails(recipients, subject, body, GMAIL_USER, GMAIL_APP_PASSWORD):
try:
        # Setup the email server
        server = smtplib.SMTP('smtp.gmail.com', 587)
        server.set_debuglevel(1)  # Enable debug output
        server.starttls()
        server.login(GMAIL_USER, GMAIL_APP_PASSWORD)

        # Send email to each recipient
        for recipient in recipients:
            msg = MIMEMultipart()
            msg['From'] = GMAIL_USER
            msg['To'] = recipient
            msg['Subject'] = subject
            msg.attach(MIMEText(body, 'plain'))
            server.sendmail(GMAIL_USER, recipient, msg.as_string())
            print(f"Email sent to {recipient}")
        
        print("All emails sent successfully!")

    except smtplib.SMTPAuthenticationError as e:
        print("Failed to authenticate. Check your Gmail ID and App Password.")
        print(e)
    except smtplib.SMTPRecipientsRefused as e:
        print("The recipient's email address was refused by the server.")
        print(e)
    except smtplib.SMTPException as e:
        print("An SMTP error occurred.")
        print(e)
    except Exception as e:
        print("An unexpected error occurred.")
        print(e)
    finally:
        # Ensure the server is always closed, whether or not an error occurred
        server.quit()

# Call the function to send the email
send_bulk_emails(recipients, subject, body, GMAIL_USER, GMAIL_APP_PASSWORD)
