---
layout: post
title: Dash app deployment on AWS Elastic Beanstalk
---

I'm writing this as a tutorial. It will be refined.

There are two primary ways to get your dash app onto AWS Elastic beanstalk.

1) Using a virtual environment.

2) Using Docker.

The processes are similar, but the virtual environment option has fewer moving parts, so I'll explain that flavor.

Ultimately, you'll need two files in a new directory somewhere on your machine:

* requirements.txt

* application.py

You can actually run this process without a virtual environment, but the virtual environment allows you to more easily set up requirements.txt, as you'll see.

In Terminal, install virtualenv and awsebcli:
```bash
pip install virtualenv
pip install awsebcli
```
awsebcli isn't necessary, but it's nice to have if you choose to deploy from command line instead of through the AWS console instead/in the future.
I'd recommend making and navigating to a new directory, but it's not strictly necessary:
```bash
mkdir eb-flask # or whatever you'd rather call the directory
cd eb-flask
```

Add your dash app to this directory and rename it application.py.

Amazon has a tutorial ([https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-flask.html#configure-your-flask-application-for-eb](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-flask.html#configure-your-flask-application-for-eb)) that I've condensed below:

Start a virtual environment:
```bash
virtualenv ~/eb-virt
source ~/eb-virt/bin/activate
```

Install flask in the virtual environment:
```bash
pip install flask
```

Run the app:
```bash
python application.py
```
You'll probably see errors about missing modules. Keep pip installing modules until this command works and the app can be seen running correctly in your browser (probably on http://127.0.0.1:5000/). 

Here are some likely ones:
```bash
pip install dash
pip install dash-core-components
pip install dash-html-components
pip install pandas
pip install numpy
```

Your virtual environment now has all the python packages installed that it needs to run the app, so we can run the following line and get a correctly set-up requirements.txt:

```bash
pip freeze > requirements.txt
```

Once you're done, you can turn off the virtual environment by deactivating it:
```bash
deactivate
```

----
Update your application.py so that it has this layout:
```python
import dash
# import whatever else you need

app = dash.Dash(__name__)
application = app.server

...

app.layout = html.Div([ ....
# and all your other code

...

if __name__ == '__main__':
    application.run(debug=True)
```
You will run into frustrating and cryptic 500 (Internal Server) Errors if you don't have the top and bottom part of your dash app (application.py) configured this way.
----
You can now start an elastic beanstalk instance on AWS and then upload a .zip file that directly contains your two files (requirements.txt and application.py), NOT the folder they are in. There are other ways to do this, but this option is the most straightforward in my opinion.
1. Go to your AWS management console
2. From AWS services, select "Elastic Beanstalk"
3. Select "Create New Application" from the upper right.
4. Configure your platform for Python
5. Upload or your code as a .zip file
6. Navigate to the URL of your site after a couple minutes of automatic EC2 set-up.

awsebcli is the alternative method for this last bit of deployment, which allows you to do it from Terminal/command line.
----    
Sources:
1. [https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-flask.html#configure-your-flask-application-for-eb](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-flask.html#configure-your-flask-application-for-eb)
2. [https://community.plot.ly/t/error-when-deploying-dash-app-on-aws-elasticbeanstalk/7567](https://community.plot.ly/t/error-when-deploying-dash-app-on-aws-elasticbeanstalk/7567)

