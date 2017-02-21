# D4a1

Problem Statement1
Write a Java program, to take a HDFS Path as input and display all the files and sub-directories in that HDFS path.

Program:


package hdfs;

import java.io.*;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.fs.FileStatus;

public class FileListing {
	public static void main(String[] args) {
		if (args.length != 1) {
			System.out.println("Pass one argument");   
			System.exit(1);
		}
		
		Path path = new Path(args[0]);
		
		try
		{
			Configuration conf = new Configuration();
			FileSystem fileSystem = FileSystem.get(path.toUri(), conf);
			FileStatus[] fileStatus=fileSystem.listStatus(path);
			
			for (FileStatus fStat : fileStatus) {
				if (fStat.isDirectory()) {                             //checking for directory
					System.out.println("Directory: " + fStat.getPath());
				}
				else if (fStat.isFile()) {                           //checking for file
					System.out.println("File: " + fStat.getPath());
				}
				else if (fStat.isSymlink()) {                         //checking for symbolic links
					System.out.println("Symlink: " + fStat.getPath());
				}
			}

		}
		catch (IOException e)
		{
            e.printStackTrace();
		}
	}
}
