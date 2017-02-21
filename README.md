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




Problem Statement2
Modify the previous program to list all the files and sub-directories in the HDFS path recursively.

Program:

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
			RemoteIterator<LocatedFileStatus> fileStatusListIterator = fs.listFiles(path, true);
    while(fileStatusListIterator.hasNext()){                          //recursively displaying directories,sub-directories and the files
        LocatedFileStatus lfs = fileStatusListIterator.next();
	System.out.println(lfs.getPath());
		}
		catch (IOException e)
		{
            e.printStackTrace();
		}
	}
}


Problem Statement3
Modify the previous program to take multiple HDFS paths (separated by space) and list all the
files and sub-directories in those HDFS paths recursively.

Program:

import java.io.*;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.fs.FileStatus;

public class FileListing {
	public static void main(String[] args) {
		
		Path[] path = new Path(args[args.length]);
		for(int i=0;i<args.length;i++)     //for multiple paths
		{
		path[i]=new Path(args[i]);
		try
		{
			Configuration conf = new Configuration();
			FileSystem fileSystem = FileSystem.get(path[i].toUri(), conf);
			RemoteIterator<LocatedFileStatus> fileStatusListIterator = fs.listFiles(path[i], true);
    while(fileStatusListIterator.hasNext()){                          //recursively displaying directories,sub-directories and the files
        LocatedFileStatus lfs = fileStatusListIterator.next();
	System.out.println(lfs.getPath());
		}
			
			

		}
		catch (IOException e)
		{
            e.printStackTrace();
		}
	}
}

