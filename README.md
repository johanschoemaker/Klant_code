# Klant_code
wat ik er tot dusver van heb gemaakt


package klant;
import  java.sql.*;
import  java.util.*;
/**
 *
 * @author Johan
 */
public class Klant {
    
    public Klant(){

    }

    
    public void createKlant(){
        Scanner input = new Scanner(System.in);
        try{ 
            Class.forName("com.mysql.jdbc.Driver");
            Connection connection = DriverManager.getConnection("jdbc:mysql//ACER/KLANT");
            
            PreparedStatement preparedstatement = connection.prepareStatement("insert into KLANT(voornaam, achternaam" 
                + "tussenvoegsel, email, straatnaam, postcode, toevoeging, huisnummer, woonplaats) values(?,?,?,?,?,?,?,?,?,?)", Statement.RETURN_GENERATED_KEYS);
            ResultSet resultSet = preparedstatement.getGeneratedKeys();
            if (resultSet.isBeforeFirst()){
                resultSet.next();
                Klant.setId(resultSet.getLong(1)); //wijs door db gegenereerde id toe aan klant
            }
            for(int i = 1; i < 10; i++){
                String temp = input.nextLine();
                 preparedstatement.setString(i, temp);
                 }
        }catch(Exception ex){
          ex.printStackTrace();
        }
    }
    
    public void readKlant(){
        Scanner input = new Scanner(System.in);
        try{ 
            Class.forName("com.mysql.jdbc.Driver");
            Connection connection = DriverManager.getConnection("jdbc:mysql//ACER/KLANT");
            
            int id = input.nextInt();
            new String[] all = {"voornaam", "achternaam" "tussenvoegsel", "email", "straatnaam", "postcode", "toevoeging", "huisnummer", "woonplaats"}; 
            
            Statement stmt = connection.createStatement();
            for(int i = 0; i < 9; i++){
                ResultSet rs = stmt.executeQuery("SELECT " + all[i] + "FROM KLANT WHERE klant_id = " + id);
            }
                 
        }catch(Exception ex){
          ex.printStackTrace();
        }
    }
    
    public void readAll(){
        try{
            Class.forName("com.mysql.jdbc.Driver");
            Connection connection = DriverManager.getConnection("jdbc:mysql//ACER/KLANT");
     
            Statement stmt = connection.createStatement();

            String sql = "SELECT voornaam, achternaam" 
                + "tussenvoegsel, email, straatnaam, postcode, toevoeging, huisnummer, woonplaats FROM KLANT";
            ResultSet rs = stmt.executeQuery(sql);
      
            ArrayList alles = new ArrayList();
            
            while(rs.next()){
         
                alles.add(rs.getString("voornaam"));
                alles.add(rs.getString("age"));
                alles.add(rs.getString("tussenvoegsel"));
                alles.add(rs.getString("email"));
                alles.add(rs.getString("straatnaam"));
                alles.add(rs.getString("postcode"));
                alles.add(rs.getString("toevoeging"));
                alles.add(rs.getString("huisnummer"));
                alles.add(rs.getString("woonplaats"));

        
            }
  
      }
        catch(Exception ex){
          ex.printStackTrace();
        //end finally try
   }//end try
    }
    
    
}
