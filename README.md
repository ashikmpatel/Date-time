# Date-time
package jdbc;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

class CurrentDateTime{
	public static void main(String[] args) {
		System.out.println("Get Current Date and Time Example...");
		Connection con = null;
		Statement statement = null;
		ResultSet rs = null;
		String url = "jdbc:mysql://localhost:3306/";
		String dbName = "students";
		String driverName = "com.mysql.jdbc.Driver";
		String userName = "root";
		String password = "root";
		try {
			// Connecting to the database
			Class.forName(driverName);
			con = DriverManager.getConnection(url + dbName, userName, password);
			try {
				// Creating object of Statement
				statement = con.createStatement();

				// Get current date and current time
				String sql = "SELECT CURDATE(),CURTIME()";
				rs = statement.executeQuery(sql);
				while (rs.next()) {
					System.out.println("Current Date : "+ rs.getDate(1));
					System.out.println("Current Time : "+ rs.getTime(2));
				}
			} catch (SQLException e) {
				System.out.println(e);
			}
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
