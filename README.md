# Chatapp
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class SendMessage {
    public static void main(String[] args) {
        try {
            // Define the URL of the messaging API
            String apiUrl = "https://example.com/api/messages"; // Replace with actual API URL
            URL url = new URL(apiUrl);
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();

            // Set request method to POST
            conn.setRequestMethod("POST");
            conn.setRequestProperty("Content-Type", "application/json");
            conn.setRequestProperty("Authorization", "Bearer YOUR_ACCESS_TOKEN"); // If authentication is needed
            conn.setDoOutput(true);

            // Message payload (replace with actual JSON format required by the API)
            String jsonInputString = "{ \"recipient\": \"user123\", \"message\": \"Hello, world!\" }";

            // Write the message to the request body
            try (OutputStream os = conn.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("utf-8");
                os.write(input, 0, input.length);
            }

            // Get the response code
            int responseCode = conn.getResponseCode();
            System.out.println("Response Code: " + responseCode);

            conn.disconnect();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
