# CRMPRO
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;

import javax.imageio.stream.FileImageInputStream;
import org.apache.poi.ss.usermodel.Cell;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.xssf.usermodel.XSSFSheet;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

public class ReadDataIntoHash {
	
	
	public void ReadData(String ExcelFile, String SheetName ) {
		
		try {
			FileInputStream fis = new FileInputStream(System.getProperty("USER_DIR"+"//"+"src//resources//"+ExcelFile));
			 XSSFWorkbook workbook = new XSSFWorkbook(fis);
			 XSSFSheet sheet = workbook.getSheet(SheetName);
			 List<HashMap<String,String>> myData = new ArrayList <HashMap<String,String>>();
			 Row HeaderRow = sheet.getRow(0);
			 
			 for (int i = 1; i<sheet.getPhysicalNumberOfRows();i++) {
				 Row currentRow = sheet.getRow(i);
				 HashMap<String, String >currentHash = new HashMap<String, String>();
				 for(int j=0;j<currentRow.getPhysicalNumberOfCells(); j++) {
					 
					Cell currentCell = currentRow.getCell(j);
					switch(currentCell.getCellType()) {
					case Cell.CELL_TYPE_STRING:
												currentHash.put(HeaderRow.getCell(j).getStringCellValue(), currentRow.getCell(j).getStringCellValue());
												break;
					case Cell.CELL_TYPE_NUMERIC:	
												currentHash.put(HeaderRow.getCell(j).getStringCellValue(), String.valueOf(currentRow.getCell(j).getNumericCellValue()));
												break;
					}	
					 
				 }
				 
			myData.add(currentHash);
			 }
			 
			 
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		
	}

}
