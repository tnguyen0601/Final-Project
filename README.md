# Final-Project
import yfinance as yf
import pandas as pd
import requests
from bs4 import BeautifulSoup
import plotly.graph_objects as go
from plotly.subplots import make_subplots
Tesla = yf.Ticker("TSLA")
Tesla_data = Tesla.history(period="max")
Tesla_data.head()
Tesla_data.reset_index(inplace=True)
beautiful_soup = BeautifulSoup(html_data, 'html5lib')
Tesla_revenue = pd.DataFrame(columns=['Date', 'Revenue'])

for table in soup.find_all('table'):

    if ('Tesla Quarterly Revenue' in table.find('th').text):
        rows = table.find_all('tr')
        
        for row in rows:
            col = row.find_all('td')
            
            if col != []:
                date = col[0].text
                revenue = col[1].text.replace(',','').replace('$','')

                Tesla_revenue = Tesla_revenue.append({"Date":date, "Revenue":revenue}, ignore_index=True)
Tesla_revenue["Revenue"] = tesla_revenue['Revenue'].str.replace(',|\$',"")
Tesla_revenue.dropna(inplace=True)

Tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != ""]
Tesla_revenue.tail()
GameStop = yf.Ticker("GME")
gme_data = gme.history(period="max")
gme_data.head()
gme_data.reset_index(inplace=True)
url = ' https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html'
html_data = requests.get(url).text
beautiful_soup = BeautifulSoup(html_data, 'html5lib')
gme_revenue = pd.DataFrame(columns=['Date', 'Revenue'])

for table in soup.find_all('table'):

    if ('GameStop Quarterly Revenue' in table.find('th').text):
        rows = table.find_all('tr')
        
        for row in rows:
            col = row.find_all('td')
            
            if col != []:
                date = col[0].text
                revenue = col[1].text.replace(',','').replace('$','')

                gme_revenue = gme_revenue.append({"Date":date, "Revenue":revenue}, ignore_index=True)
gme_revenue.tail()
make_graph(tesla_data, tesla_revenue, 'Tesla')
make_graph(gme_data, gme_revenue, 'GameStop')
