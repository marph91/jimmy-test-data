Able to extract sudomains from the crtsh site

the below code used to extract subdomains from the site 

1. Paste the below code into the browser console
2. The subdomains downloaded as text file


(function() {
    // Create a Blob to save the data as a file
    let subdomains = [];
    
    // Extract all subdomains from the "Matching Identities" column (index 5)
    let rows = document.querySelectorAll('table tr');
    rows.forEach(function(row) {
        let cells = row.getElementsByTagName('td');
        if (cells.length > 5) {
            // Extract the subdomain data from the 6th column (index 5)
            let subdomainData = cells[5].innerText.trim();
            // Split the subdomain data into individual subdomains
            let subdomainList = subdomainData.split('\n');
            subdomains = subdomains.concat(subdomainList);
        }
    });

    // Remove any empty strings from the array
    subdomains = subdomains.filter(subdomain => subdomain.trim() !== '');

    // Create a Blob from the array of subdomains
    let blob = new Blob([subdomains.join('\n')], { type: 'text/plain' });

    // Create a download link
    let link = document.createElement('a');
    link.href = URL.createObjectURL(blob);
    link.download = 'crtsh_subdomains.txt';

    // Trigger the download
    link.click();
})();
