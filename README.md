# Kali Linux to DigitalOcean

This GitHub Action automates the process of downloading, converting, and uploading the latest **Kali Linux Generic Cloud Image** to **Custom Images in DigitalOcean**.

## Features

- Automatically downloads the latest Kali Linux Generic Cloud Image.
- Converts and compresses the image for compatability with DigitalOcean.
- Uploads the compressed image to DigitalOcean's Custom Images using the DigitalOcean API.
- Versioning is maintained and incremented automatically for each upload.

## Usage

### 1. Fork the Repository

1. Click the **Fork** button at the top of the GitHub repository page.
2. Once forked you can use it directly from your account.

### 2. Secrets Setup

You'll need to create the following secrets in your forked repository for the action to work:

1. **`DIGITALOCEAN_ACCESS_TOKEN`**: Your DigitalOcean API token. You can generate it in your DigitalOcean API settings.
    1. Create A New Personal Access Token and give the token a name.
    2. Choose **Custom Scopes** then the only scope needed is **Image > Create**.
2. **`REGION`**: The DigitalOcean region where you'd like the image to be uploaded (e.g., `nyc3`, `sfo3`, etc.). The valid region slugs are listed in the DigitalOcean API documentation.

To add these secrets:

1. Go to your forked repository on GitHub.
2. Navigate to **Settings** > **Secrets and variables** > **Actions**.
3. Click **New repository secret** and add `DIGITALOCEAN_ACCESS_TOKEN` and `REGION`.

### 3. Workflow Permissions

Once you fork the repository, you'll need to update your **workflow permissions** to allow the action to commit and push changes:

1. Go to **Settings > Actions > General** in your forked repository.
2. Under **Workflow permissions**, select **"Read and write permissions"**.
3. Check the box for **"Allow GitHub Actions to create and approve pull requests"**.

### 4. Running the Workflow

Once your secrets and workflow permissions are set, you can manually trigger the workflow:

1. Navigate to the **Actions** tab of your repository.
2. Select **Kali Linux to DigitalOcean** from the left-hand sidebar.
3. Click **Run workflow** under the **workflow_dispatch** section.

> [!WARNING]  
> **DigitalOcean Processing**: Occasionally, DigitalOcean's backend can take longer to process and validate the image, especially during peak times. It may take up to 10 minutes or more for the image to be marked as **Available**. If the image remains stuck in **Pending**, delete the image in DigitalOcean and try again, or try changing the region. To change the region, update the `REGION` secret in your GitHub repository to a different valid region (e.g., `nyc3`, `sfo3`).

> [!TIP]
> After the workflow completes, you can manually upload the `disk.raw.gz` file in the release files to DigitalOcean. This is useful if you want to manually upload the image without rerunning the workflow:
>
> 1. Go to **Backups & Snapshots** > **Custom Images** in the DigitalOcean dashboard.
> 2. Choose **Import via URL** and provide the release URL for the `disk.raw.gz` file from your GitHub repository.

## Creating a Droplet from the Custom Image

After the image is available in DigitalOcean, you can create a droplet from it:

1. Go to **Droplets** in your DigitalOcean dashboard.
2. Select **Create Droplet**.
3. Under **Choose an image**, select **Custom Images**.
4. Select the Kali Linux image you uploaded.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.
