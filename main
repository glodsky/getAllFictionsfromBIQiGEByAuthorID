import requests
from lxml import etree
import time
headers = {
    'user-agent': 'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36'
    } 
    
def get_OnePage(capter,url):
    response = requests.get(url,headers=headers)
    if response.status_code ==200:
        html = response.content
        paser = etree.HTML(html)        
        print 'Getting: '+ capter + '  ' + url
        data = paser.xpath('//div[@id="content"]/text()')
        content = "\n".join(data).encode("utf8")
        #print content
        if len(content)>0:
            with open('./%s.txt'%capter,'w+') as f:
                f.write(content)
                f.close()
                print "Saved : %s.txt\n"%capter
        else:
            print "Content is nothing at :" + capter
        
        

def get_AllChapersUrls(main_url):
    urls = {}
    response = requests.get(main_url,headers=headers)
    if response.status_code == 200:
        html = response.content
        paser = etree.HTML(html)
        title = paser.xpath('title/text()')         
        alist = paser.xpath('//div[@id="list"]/dl/dd/a')
        for x in alist:
            atext = x.text
            ahref = x.attrib['href']
            urls[atext]="https://www.xbiquge6.com"+ahref
            print urls[atext]
    return urls


def main():
    target = 'https://www.xbiquge6.com/77_77763/'
    urls = get_AllChapersUrls(target)
    count = 0
    for (k,v) in urls.items():
        get_OnePage(k,v)
        count = count + 1
        if count % 20 == 0 :
            print "Sleep 2 secods . Waiting ...."
            time.sleep(2)

if __name__ == '__main__':
    main()
    #get_OnePage("Test","https://www.xbiquge6.com/77_77763/1230887.html")
 

    
