# Crawling Subtitles from HK Movies

## File Description

+ "crawling_subtitles.ipynb" contains the codes for crawling and processing movie subtitles.
+ "processed" folder contains all processed subtitles texts.
+ "all_filtered_subtitles" folder contains the original subtitle files.
+ "output/id_name_dict.json" is the dictionary mapping the movie id to its movie name.
+ "original_movie_list" folder contains the original movie list downloaded from wikipedia (more details below)

## Data Source

Subtitles are crawled from http://assrt.net/. 

Note: APIs are provided for personal use. We need to contact admin@assrt.net for commercial use. 

API details: http://assrt.net/api/doc#subs
+ It provides APIs for：
   + searching using keywords (API 1),
   + requesting details using movie id (API 2), 
   + and searching similar movie subtitles using movie id (API 3).  
   Note: only API 1 and API 2 are used in our implementation
+ The number of requests is limited to 20 per minute. 

## How to obtain subtitles for massive movies?

We consider two approaches.   
+ One is to obtain a name list for HK Movies first. Then we use the name list to request the movie id using API 1 and use the returned movie id to request subtitle details (including download url). Finally we use the url to download the subtitle files. One limitation for this approach is that the selected name list may not be compact.  
+ Another is to go through all movies using all possible movie ids (6 digits, i.e., 0-999999) and identify which ones are in traditional Chinese. One limitation for this approach is the computational waste [1000000/20 = 50000 min = 833 hours are required to complete all requests due to the API request limit].

We utilized the first approach in our implementation.  

Details:

The name list for HK Movies (from Wikipedia)：
+ a whole list regardless of years: [List 1](https://zh.wikipedia.org/zh-hk/%E9%A6%99%E6%B8%AF%E9%9B%BB%E5%BD%B1%E5%88%97%E8%A1%A8), processed list is in original_movie_list/MovieList.xlsx
+ a list of HK Movies in decades: [List 2](https://zh.wikipedia.org/zh-hk/Category:%E5%90%84%E5%B9%B4%E4%BB%A3%E9%A6%99%E6%B8%AF%E9%9B%BB%E5%BD%B1%E4%BD%9C%E5%93%81), processed list is in original_movie_list/MovieListYearly.xlsx
+ a list of HK Movies in various years: [List 3](https://zh.wikipedia.org/wiki/Category:%E5%90%84%E5%B9%B4%E9%A6%99%E6%B8%AF%E9%9B%BB%E5%BD%B1%E4%BD%9C%E5%93%81%E5%88%97%E8%A1%A88) (not adopted)  
 
The lists are in the "./original_movie_list" folder.

# Statistics
| List | Num. of movies in the list | Num. of movies crawled | Num. of movies with trad zh subtitles | Num. of Movies after processing | Num. of tokens |
| :----: | :----: | :----: | :----: | :----: | :----: |
| List 1 | 388 | 130 | 126 | 91 | 1,184,467 |
| List 2 | 1197 | 412 | 405 | 200 | 3,958,373 |
| all | 1399 | 463 | 444 | 291 | 5,142,840 |


