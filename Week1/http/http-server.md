```sh
import java.util.Date;
import java.net.*;
import java.io.*;

public class TimeServer {
public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(8080);
        System.out.println("Listening on port 8080...");
        while (true) {
            try (Socket clientSocket = serverSocket.accept()) {
                OutputStreamWriter osw = new OutputStreamWriter(clientSocket.getOutputStream(), "UTF-8");
                String response = "Current time: " + new Date().toString();
                osw.write("HTTP/1.1 200 OK\r\n");
                osw.write("Content-Type: text/plain; charset=UTF-8\r\n");
                osw.write("Content-Length: " + response.length() + "\r\n");
                osw.write("\r\n");
                osw.write(response);
                osw.flush();
                System.out.println("Response sent:\n" + response);
            } catch (IOException e) {
                System.err.println("Error handling request: " + e.getMessage());
            }
        }
    }
}
```

**Result**

> Current time: Tue Feb 28 08:40:04 ICT 2023
