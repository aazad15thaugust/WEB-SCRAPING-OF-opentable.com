# WEB-SCRAPING-of-londontable.com
import requests

from bs4 import BeautifulSoup

url = 'https://www.opentable.com/start/?m=72'

opentable_r = requests.get(url)

#opentable_r -- <Response 200>

print(opentable_r.status_code) #200

opentable_soup = BeautifulSoup(opentable_r.text,'html.parser')

print(opentable_soup.prettify())

print(opentable_soup.findAll('h3'))

restaurent = opentable_soup.findAll('div',{'class': "_81940a74 b2f6d1a4"})

for restro in  restaurent:

	#print(restro.text)
	
	name = restro.findAll('h3',{'class': "edec43ac _2a03da4e"})[0].text
	
        print(name)
	
	reviews = restro.findAll('span',{'class':"ab66eedc _965a91d5"})[0].text
	
	print(reviews)
	
	type = restro.findAll('span',{'class':"_37b568e3"})[0].text
	
	print(type)
	
	print('\n')

file_path = 'opentable.txt'

with open(file_path, "a") as  textfile:

	restaurent = opentable_soup.findAll('div',{'class': "_81940a74 b2f6d1a4"})
	
	for restro in  restaurent:
	
        	#print(restro.text)
		
        	name = restro.findAll('h3',{'class': "edec43ac _2a03da4e"})[0].text
		
        	print(name)
		
        	reviews = restro.findAll('span',{'class':"ab66eedc _965a91d5"})[0].text
		
        	print(reviews)
		
        	type = restro.findAll('span',{'class':"_37b568e3"})[0].text
		
        	print(type)
		
        	print('\n')
		
		page_line = "{name}\n{reviews}\n{type}\n\n".format(
		
			name=name,
			
			reviews=reviews,	
			
			type=type,
			
			)
			
		print('\n')
		
		textfile.write(page_line)
