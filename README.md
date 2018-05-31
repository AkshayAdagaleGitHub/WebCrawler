# WebCrawler
Web Crawler in Java using jsoup.jar


import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class webcrawler {

 public webcrawler()
	{	
	
  }
	
	public void FetchAndWriteToFile(String url) throws IOException{

		//Connecting with the URL
		Document document = Jsoup.connect(url).userAgent("Mozilla").get();
		Elements elements = document.select("h1");
		
		//Creating new File 
		FileWriter fstream = new FileWriter("d://text2.txt",true);
		BufferedWriter out = new BufferedWriter(fstream);
		
		//Selecting a div tag with class name bckSolidWht bckPadLarge clearfix ( eg: <div class=bckSolidWht bckPadLarge clearfix>)
		Elements inside = document.select("div[class=bckSolidWht bckPadLarge clearfix]");
		
		//writing the string inside div tag and what ever tag is present inside (It will skip all the tags and only fetch the string) into         the file
		out.write(inside.text());
		
		//Printing the string inside the div tag
		System.out.println(inside.text());
		
		//Writing the title inside a file
		out.write(elements.text().replace(".", " "));
		
		out.close();
		
	}
	

	public static void main(String[] args) throws IOException {
		new webcrawler().FetchAndWriteToFile("Please enter your url"); //eg:https://www.symantec.com/security_response/writeup.jsp?docid=2018-020911-3250-99
	}

}
