Class to import songs
=============
import java.io.File;
import java.io.IOException;

import org.apache.commons.io.FileUtils;

public class TestImport
{

    private final static File rootDirectory = new File("C:\\USB");

    public static void main(String[] args)
    {
        TestImport import1 = new TestImport();
        import1.copyDirectory(rootDirectory);
    }

    public void copyDirectory(File directory)
    {
        System.out.println("Directory being worked on " + directory.getName());
        File[] listOfFiles = directory.listFiles();
        for (File file : listOfFiles)
        {
            if (file.isFile())
            {
                if (file.getName().contains(".mp3") && !file.getParent().equals("C:\\USB"))
                {
                    try
                    {
                        System.out.println("File being copied " + file.getName());
                        FileUtils.copyFileToDirectory(file, rootDirectory);
                    }
                    catch (IOException e)
                    {
                        e.printStackTrace();
                    }
                }
            }
            else if (file.isDirectory() && !file.equals(rootDirectory))
            {
                copyDirectory(file);
            }

        }
    }

}
