package readxmlstax;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.Iterator;

import javax.xml.stream.XMLEventReader;
import javax.xml.stream.XMLInputFactory;
import javax.xml.stream.XMLStreamConstants;
import javax.xml.stream.XMLStreamException;
import javax.xml.stream.events.Attribute;
import javax.xml.stream.events.Characters;
import javax.xml.stream.events.EndElement;
import javax.xml.stream.events.StartElement;
import javax.xml.stream.events.XMLEvent;

public class StAXParserDemo {
   public static void main(String[] args) throws ClassNotFoundException, InstantiationException, IllegalAccessException, SQLException {
      boolean bFirstName = false;
      boolean bLastName = false;
      boolean bNickName = false;
      boolean bMarks = false;
      ArrayList<String> allcols = new ArrayList<String>();
  	
  	allcols = getcolnames();
  	boolean hasvalue=false;
  	boolean colbool[] = new boolean[allcols.size()];
  	for(int i=0; i<allcols.size(); i++){
  		colbool[i] = false;	
  	}
  	
  	
      try {
         XMLInputFactory factory = XMLInputFactory.newInstance();
         XMLEventReader eventReader =
         factory.createXMLEventReader(
            new FileReader("D:/serviceRocket/serviceRocket_lead.xml"));
         String columnName = "";
         String columnValue="";
         String attrval="";
         String insertStatement_A = "";
         String insertStatement_B = "";
         String insertStatement_C="";
         String insertStatement_full="";
         boolean isnull = false;
         ArrayList<String> insertColnames = new ArrayList<String>();
         ArrayList<String> insertValues = new ArrayList<String>();
         Connection ds             = null;
	        String dbName = "";
	        //dbName = "quarrio"+userid+"_cache";
	         ds = createConnection();
         
         int count = 0;
            while(eventReader.hasNext()){
            
            	XMLEvent event = eventReader.nextEvent();
               switch(event.getEventType()){
                  case XMLStreamConstants.START_ELEMENT:
                     StartElement startElement = event.asStartElement();
                     String qName = startElement.getName().getLocalPart();
                     if (qName.equalsIgnoreCase("records")) {
                    	 insertColnames.clear();
                    	 insertValues.clear();
                       // System.out.println("-----------------------Start Element : records----------------------");
                      insertStatement_A="insert into \"Leadtest\"(";
           			  insertStatement_B=") values(";
           			  insertStatement_C=" )";
           			  insertStatement_full="";
                     }
                     
                     for(int i=0; i<allcols.size(); i++)
                    	 
                     { if (qName.equalsIgnoreCase(allcols.get(i))) {
                       	 colbool[i] = true;
                     
                     Iterator<Attribute> attributes = startElement.getAttributes();
                    	 columnName = allcols.get(i);
                    	 attrval="false";
                    	 if(attributes.hasNext()){
                    		 isnull = true;
                    		 colbool[i] = false;
                    		 columnName=allcols.get(i);
                             columnValue=null;
                             insertColnames.add(columnName);
                             insertValues.add(columnValue);
                             
                             //System.out.println("col name: "+columnName+" : col Value :"+ columnValue);
                            /* insertStatement_A += "\""+columnName+"\", ";
        					 if(columnValue==null){
        						 insertStatement_B += ""+columnValue+", ";
        					 }
        					 else{
        						 columnValue = columnValue.replace("'", "");
        					 insertStatement_B += "'"+columnValue+"', ";
        					 }*/
                             
                    		 
                    		 
                    		 }
                     
                     }		
                     }
                     break;
                  case XMLStreamConstants.CHARACTERS:
                     Characters characters = event.asCharacters();
                     for(int i=0; i<allcols.size(); i++){
                     if(colbool[i]){
                    	
        
                    	
                    		 columnName=allcols.get(i);
                             columnValue=characters.getData();
                             
                             //add col name and vals to array list
                             insertColnames.add(columnName);
                             insertValues.add(columnValue);
                             
                             //System.out.println("col name: "+columnName+" : col Value :"+ columnValue);
                             /*insertStatement_A += "\""+columnName+"\", ";
        					 if(columnValue==null){
        						 insertStatement_B += ""+columnValue+", ";
        					 }
        					 else{
        						 columnValue = columnValue.replace("'", "");
        					 insertStatement_B += "'"+columnValue+"', ";
        					 }*/
                    	
                    	
                        colbool[i] = false;
                        
                        
                        
                    	
                    	 }
                     
                     }
                     break;
                  case  XMLStreamConstants.END_ELEMENT:
                     EndElement endElement = event.asEndElement();
                     if(endElement.getName().getLocalPart().equalsIgnoreCase("records")){
                        //System.out.println("----------------------------End Element : records---------------------------");
                        System.out.println(": "+count);
                        count = count + 1;
                       /* insertStatement_A=insertStatement_A.replaceAll(", $", "");
                        
                        
                        
                        //System.out.println(insertStatement_A);
       				    insertStatement_B=insertStatement_B.replaceAll(", $", "");
       				   // System.out.println(insertStatement_B);
       				    //System.out.println("Row count: " +j);
       				    insertStatement_full = insertStatement_A + insertStatement_B + insertStatement_C;
       				  */
       				    //System.out.println(insertStatement_full);
       				  //  System.out.println("--col names--");
       				    //System.out.println(insertColnames);
       				    //System.out.println("---col values ----");
       				    //System.out.println(insertValues);
       				    
       				    //System.out.println(insertColnames.get(0));
       				    
       				    //remove default tags type/id, there are 2 so we will make two alterations
       				    for(int a=0; a<2;a++){
       				    if((insertColnames.get(0).equals("Id")) || (insertColnames.get(0).equals("Type"))){
       				    	insertColnames.remove(0);
       				    	insertValues.remove(0);
       				    }
       				    }
       				 //System.out.println("--col names--");
    				   // System.out.println(insertColnames);
    				  //  System.out.println("---col values ----");
    				   // System.out.println(insertValues);
    				    
    				    //make query
       				    for(int i=0; i<insertColnames.size(); i++){
       				    	
       				    	


       				    	insertStatement_A += "\""+insertColnames.get(i)+"\", ";
       					 if(insertValues.get(i)==null){
       					//	 System.out.println("value is null");
       						 insertStatement_B += ""+insertValues.get(i)+", ";
       					 }
       					 else{
       						//insertValues.get(i) = insertValues.get(i).replace("'", "");
       					 insertStatement_B += "'"+insertValues.get(i).replace("'", "")+"', ";
       					 }	       				    	
       				    }//for end
       				  
       				 insertStatement_A=insertStatement_A.replaceAll(", $", "");
                    
    				 insertStatement_B=insertStatement_B.replaceAll(", $", "");
    				  
    				 insertStatement_full = insertStatement_A + insertStatement_B + insertStatement_C;
    				
    				 //System.out.println(insertStatement_full);
       				    
       				    insertData(insertStatement_full, ds);
                        
                        //System.out.println();
                     }
                     break;
               }		    
            }
         } catch (FileNotFoundException e) {
            e.printStackTrace();
         } catch (XMLStreamException e) {
            e.printStackTrace();
      }
   }

   
   public static void insertData(String insertQuery, Connection ds) throws SQLException{
		java.sql.Statement  stmt  = null;
		stmt = ds.createStatement();
		
		stmt.executeUpdate(insertQuery);
		
		
	}
   
   
   public static ArrayList<String> getcolnames() throws ClassNotFoundException, InstantiationException, IllegalAccessException, SQLException{
		
		ArrayList<String> allcols = new ArrayList<String>();
		allcols.clear();
		
		Connection ds             = null;
	    java.sql.Statement  stmt  = null;
	    String dbName = "";
	    //dbName = "quarrio"+userid+"_cache";
	     ds = createConnection();
	     stmt = ds.createStatement();
	     
	     String colQuery="SELECT column_name FROM information_schema.columns WHERE table_schema = 'public'  AND table_name   = 'Leadtest'";
	     
	     ResultSet rs = stmt.executeQuery(colQuery);
	     while(rs.next()){
	    	 //System.out.println(rs.getString("column_name"));
	    	 String colname=rs.getString("column_name");
	    	 //add col to arraylist
	    	 allcols.add(colname);
	    	 //String resulttag= getString(rs.getString("column_name"), rootElement,1);
	    	 
	    	// System.out.println("---------------------taq result----------------");
	    	// System.out.println(resulttag);
	    	// System.out.println("---------------------taq result End----------------");
	     }
	     //System.out.println(allcols);
	     System.out.println("column size : "+allcols.size());
	     return allcols;
	     
	}



	public static Connection createConnection()
	        throws ClassNotFoundException, InstantiationException, IllegalAccessException, SQLException {
	    Connection         c;
	    
	    String DbName = "quarrio005A0000005BIXjIAO_cache";

		//Class.forName("com.mysql.jdbc.Driver").newInstance();
	    //c = DriverManager.getConnection("jdbc:mysql://52.66.99.31/" + DbName , "usman", "22crimes");
	    
	    // Register Postgresql driver
		Class.forName("org.postgresql.Driver");
		c = DriverManager.getConnection("jdbc:postgresql://staging-rds.conversationanalytics.io/" + DbName , "mypostgres", "L0LinSL2017");

		System.out.println("connection established.");
	    return c;
	}


}

